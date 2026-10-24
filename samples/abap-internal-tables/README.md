# ABAP 内表与 SQL：五章样本

这份样本从个人 ABAP 学习笔记中的“内表”主题挑选内容，整理为五章，适合快速了解 ABAP 内表的声明、访问、SQL 查询和常见排查思路。示例已改用通用对象名；未包含私人 Obsidian 路径、原始截图或特定项目对象。

> 这是个人学习资料，不是 SAP 官方教材。代码片段用于说明思路；请按目标 ABAP 产品和版本核对语法，并替换示例中的表名、字段名和类型。

## 目录

1. [定义行类型和内表](#chapter-1)
2. [选择内表类型和键](#chapter-2)
3. [追加、读取和排序](#chapter-3)
4. [用 ABAP SQL 查询和关联数据](#chapter-4)
5. [排查输出行数变少](#chapter-5)

<a id="chapter-1"></a>
## 第 1 章：定义行类型和内表

内表由行类型、表类别和键共同决定。先定义每行有哪些字段，再声明保存多行数据的内表：

```abap
TYPES:
  BEGIN OF ty_item,
    item_id  TYPE n LENGTH 6,
    category TYPE c LENGTH 10,
    amount   TYPE p LENGTH 8 DECIMALS 2,
  END OF ty_item.

DATA lt_items TYPE STANDARD TABLE OF ty_item WITH EMPTY KEY.
DATA ls_item  TYPE ty_item.
```

`ty_item` 描述单行结构，`lt_items` 保存多行，`ls_item` 保存一行。`WITH EMPTY KEY` 表示此标准表不依赖默认主键；需要按字段查找时，在读取语句中明确给出条件。

<a id="chapter-2"></a>
## 第 2 章：选择内表类型和键

根据主要访问方式选择表类别。下面三种声明使用同一个行类型：

```abap
DATA lt_standard TYPE STANDARD TABLE OF ty_item
                  WITH EMPTY KEY.

DATA lt_sorted TYPE SORTED TABLE OF ty_item
                WITH NON-UNIQUE KEY category item_id.

DATA lt_hashed TYPE HASHED TABLE OF ty_item
                WITH UNIQUE KEY item_id.
```

| 表类别 | 适合的访问方式 | 需要注意 |
| --- | --- | --- |
| `STANDARD TABLE` | 顺序处理、按索引处理 | 不会因声明自动按字段排序；按普通键查找通常要逐行检查。 |
| `SORTED TABLE` | 按键排序、按键前缀范围读取 | 插入后由键顺序维护行序；可使用唯一或非唯一键。 |
| `HASHED TABLE` | 反复按完整唯一键查单行 | 键必须唯一；没有主索引，不能按行号读取。 |

不要只凭“哪种最快”选择表类型。访问模式、键的组成、数据量和更新频率都会影响实际表现；二次键也会增加内存和维护成本。

<a id="chapter-3"></a>
## 第 3 章：追加、读取和排序

标准表可以顺序追加。读取成功后，`sy-subrc` 为 `0`；此时可以通过字段符号直接修改找到的行：

```abap
APPEND VALUE #(
  item_id  = '000001'
  category = 'A'
  amount   = '12.50'
) TO lt_standard.

READ TABLE lt_standard ASSIGNING FIELD-SYMBOL(<item>)
  WITH KEY item_id = '000001'.

IF sy-subrc = 0.
  <item>-amount = <item>-amount + 1.
ENDIF.
```

如果在标准表上使用 `BINARY SEARCH`，必须先按查找键的**相同字段顺序升序排序**：

```abap
SORT lt_standard BY category item_id.

READ TABLE lt_standard INTO DATA(ls_found)
  WITH KEY category = 'A'
           item_id  = '000001'
  BINARY SEARCH.
```

排序顺序与查找键不一致时，二分查找可能找不到实际存在的行。新代码可以考虑直接用排序表或显式二次键表达访问意图，避免依赖手工排序约定。

<a id="chapter-4"></a>
## 第 4 章：用 ABAP SQL 查询和关联数据

`INTO TABLE` 把一组查询结果接收到内表。`JOIN` 可把符合关联条件的多个数据源合并为一个结果集：

```abap
SELECT FROM your_header AS h
       INNER JOIN your_item AS i
         ON i~document_id = h~document_id
       FIELDS h~document_id,
              i~item_id,
              i~amount
       WHERE h~status = @lv_status
       INTO TABLE @DATA(lt_result).
```

把 `your_header`、`your_item` 和字段名换成目标系统中可用的数据源。`AS` 为数据源设置别名，`~` 用来标明字段来自哪个数据源。`INNER JOIN` 只保留匹配成功的行；改用 `LEFT OUTER JOIN` 时会保留左侧行，右侧没有匹配时其字段为空值。

如果只是取得一批数据，优先一次查询到内表，再在内存中处理；不要不加判断地在 `LOOP` 内逐行执行数据库查询，以免造成大量重复访问。

<a id="chapter-5"></a>
## 第 5 章：排查输出行数变少

`READ TABLE` 负责查找，不会删除来源内表。查找结果经常通过 `sy-subrc` 控制后续的 `APPEND`：

以下代码假设主记录带有 `id`、`amount`，查找表以 `id` 为唯一键，输出类型含 `id`、`label` 和 `amount`：

```abap
TYPES:
  BEGIN OF ty_main,
    id     TYPE c LENGTH 10,
    amount TYPE p LENGTH 8 DECIMALS 2,
  END OF ty_main.
TYPES ty_main_tab TYPE STANDARD TABLE OF ty_main WITH EMPTY KEY.

TYPES:
  BEGIN OF ty_lookup,
    id    TYPE c LENGTH 10,
    label TYPE c LENGTH 30,
  END OF ty_lookup.
TYPES ty_lookup_tab TYPE HASHED TABLE OF ty_lookup WITH UNIQUE KEY id.

TYPES:
  BEGIN OF ty_out,
    id     TYPE c LENGTH 10,
    label  TYPE c LENGTH 30,
    amount TYPE p LENGTH 8 DECIMALS 2,
  END OF ty_out.
TYPES ty_out_tab TYPE STANDARD TABLE OF ty_out WITH EMPTY KEY.

DATA lt_main   TYPE ty_main_tab.
DATA lt_lookup TYPE ty_lookup_tab.
DATA gt_output TYPE ty_out_tab.
```

```abap
LOOP AT lt_main INTO DATA(ls_main).
  DATA(ls_out) = VALUE ty_out(
    id     = ls_main-id
    amount = ls_main-amount
  ).

  READ TABLE lt_lookup INTO DATA(ls_lookup)
    WITH TABLE KEY id = ls_main-id.

  IF sy-subrc = 0.
    ls_out-label = ls_lookup-label.
  ENDIF.

  APPEND ls_out TO gt_output.
ENDLOOP.
```

这段逻辑把所有 `lt_main` 主记录都追加到输出；找不到对应项时，`label` 保持初始值。若把 `APPEND` 放进 `IF sy-subrc = 0`，输出就只保留匹配成功的行，效果接近 `INNER JOIN`。保留主记录的逻辑则接近 `LEFT OUTER JOIN`。

输出条数不符合预期时，依次检查：

1. 数据库查询结果和循环输入表的行数。
2. `READ TABLE` 后立即检查的 `sy-subrc`。
3. `APPEND` 是否被 `IF`、`CHECK` 或 `CONTINUE` 控制。
4. 业务要求是保留全部主记录，还是只输出匹配行。
5. 最后确认界面或报表读取的是正确的输出内表。

## 官方参考

- [Creating Internal Tables](https://help.sap.com/docs/abap-cloud/abap-concepts/how-to-create-internal-tables-locally)
- [Selecting the Table Category](https://help.sap.com/docs/abap-cloud/abap-keyword/itab-selection-of-table-category?locale=en-US&state=PRODUCTION&version=latest)
- [Populating Internal Tables](https://help.sap.com/docs/abap-cloud/abap-concepts/populating-internal-tables)
- [READ TABLE, free_key](https://help.sap.com/docs/abap-cloud/abap-keywords/read-table-free-key)
- [SELECT, FROM JOIN](https://help.sap.com/docs/abap-cloud/abap-keywords/select-from-join)
