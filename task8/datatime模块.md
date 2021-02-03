# datetime模块

datetime 是 Python 中**处理日期的标准模块**，它提供了 4 种对日期和时间进行处理的类：**datetime**、**date**、**time** 和 **timedelta**。

- `datetime.now(tz=None)` 获取当前的日期时间，输出顺序为：年、月、日、时、分、秒、微秒。
- `datetime.timestamp()` 获取以 1970年1月1日为起点记录的秒数。
- `datetime.fromtimestamp(tz=None)` 使用 unixtimestamp 创建一个 datetime。

- `datetime.strftime(fmt)` 格式化 datetime 对象。

| 符号 | 说明                                           |
| ---- | ---------------------------------------------- |
| `%a` | 本地简化星期名称（如星期一，返回 Mon）         |
| `%A` | 本地完整星期名称（如星期一，返回 Monday）      |
| `%b` | 本地简化的月份名称（如一月，返回 Jan）         |
| `%B` | 本地完整的月份名称（如一月，返回 January）     |
| `%c` | 本地相应的日期表示和时间表示                   |
| `%d` | 月内中的一天（0-31）                           |
| `%H` | 24小时制小时数（0-23）                         |
| `%I` | 12小时制小时数（01-12）                        |
| `%j` | 年内的一天（001-366）                          |
| `%m` | 月份（01-12）                                  |
| `%M` | 分钟数（00-59）                                |
| `%p` | 本地A.M.或P.M.的等价符                         |
| `%S` | 秒（00-59）                                    |
| `%U` | 一年中的星期数（00-53）星期天为星期的开始      |
| `%w` | 星期（0-6），星期天为星期的开始                |
| `%W` | 一年中的星期数（00-53）星期一为星期的开始      |
| `%x` | 本地相应的日期表示                             |
| `%X` | 本地相应的时间表示                             |
| `%y` | 两位数的年份表示（00-99）                      |
| `%Y` | 四位数的年份表示（0000-9999）                  |
| `%Z` | 当前时区的名称（如果是本地时间，返回空字符串） |
| `%%` | %号本身                                        |

- `datetime.date()` Return the date part.
- `datetime.time()` Return the time part, with tzinfo None.
- `datetime.year` 年
- `datetime.month` 月
- `datetime.day` 日
- `datetime.hour` 小时
- `datetime.minute` 分钟
- `datetime.second` 秒
- `datetime.isoweekday` 星期几

datetime 对象包含很多与日期时间相关的实用功能。

```python
import datetime

dt = datetime.datetime(year=2020, month=6, day=25, hour=11, minute=51, second=49)
print(dt.date())  # 2020-06-25
print(type(dt.date()))  # <class 'datetime.date'>
print(dt.time())  # 11:51:49
print(type(dt.time()))  # <class 'datetime.time'>
print(dt.year)  # 2020
print(dt.month)  # 6
print(dt.day)  # 25
print(dt.hour)  # 11
print(dt.minute)  # 51
print(dt.second)  # 49
print(dt.isoweekday())  # 4
```

在处理含有字符串日期的数据集或表格时，我们需要一种**自动解析字符串**的方法，无论它是什么格式的，都可以**将其转化为 datetime 对象**。这时，就要使用到 dateutil 中的 parser 模块。

- `parser.parse(timestr, parserinfo=None, **kwargs)`

```python
from dateutil import parser

s1 = "2010 Jan 1"
s2 = '31-1-2000'
s3 = 'October10, 1996, 10:40pm'

dt1 = parser.parse(s1)
dt2 = parser.parse(s2)
dt3 = parser.parse(s3)

print(dt1)  # 2010-01-01 00:00:00
print(dt2)  # 2000-01-31 00:00:00
print(dt3)  # 1996-10-10 22:40:00
```

- `date.today()` 获取当前日期信息。

`timedelta` 表示具体时间实例中的一段时间。你可以把它们简单想象成两个日期或时间之间的间隔。

它常常被用来从 `datetime` 对象中添加或移除一段特定的时间。

```python
td1 = datetime.timedelta(days=30)  # 30 days
td2 = datetime.timedelta(weeks=1)  # 1 week
td = td1 - td2
print(td)  # 23 days, 0:00:00
print(type(td))  # <class 'datetime.timedelta'>
```

如果将两个 datetime 对象相减，就会得到表示该时间间隔的 timedelta 对象。

同样地，将两个时间间隔相减，可以得到另一个 timedelta 对象。

```python
import re
from datetime import datetime, timezone, timedelta

def to_timestamp(dt_str, tz_str):
    # 首先，获取用户输入的时间的datetime
    input_dt = datetime.strptime(dt_str, '%Y-%m-%d %H:%M:%S')

    # 上面得到的datetime是没有时区的，因此设置用户输入的对应时区
    # 那么此时需要利用正则获取用户输入的时区
    time_zone_num = re.match(r'UTC([+|-][\d]{1,2}):00', tz_str).group(1)
    time_zone = timezone(timedelta(hours=int(time_zone_num)))  # 创建时区UTC-？？
    
    # 将上面得到的datetime强制设置为UTC-？？
    input_dt_tz = input_dt.replace(tzinfo=time_zone)
    
    return input_dt_tz.timestamp()

# 测试:

t1 = to_timestamp('2015-6-1 08:10:30', 'UTC+7:00')
assert t1 == 1433121030.0, t1

t2 = to_timestamp('2015-5-31 16:10:30', 'UTC-09:00')
assert t2 == 1433121030.0, t2

print('ok')
```

1. ```python
    import datetime 
     
    a = int(input())
       
   def all_sundays(year):
      
      dt1=datetime.date(a,1,1)
      dt2=datetime.date(a,12,31)
       for i in range((dt2-dt1).days+1):
          day=dt1+datetime.timedelta(days=i)
          b=day.isoweekday()
           if b==7:
               print(day)
          else:
             continue       
   all_sundays(a)
   ```

   
