This document introduces the basic syntax and examples of nested subqueries.

>? CLS functions are currently available only in the Chongqing region. To make them available to other regions, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>

## Overview

For some complex query scenarios, single-level SQL queries are insufficient, and nested SQL queries are required.

Different from an unnested query, a nested subquery requires the FROM condition to be specified in the SQL statement. The `from log` keywords must be specified in a query to read raw data from the log.


## Example

```
* | select sum(status) from 
(
select status, count(1) as pv from log group by status limit 2000
)
```

