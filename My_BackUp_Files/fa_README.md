<style>
/* تنظیمات عمومی برای راست‌چین کردن تمام متن‌ها */
* {
    direction: rtl;
    text-align: right;
    font-family: 'Vazir', 'Tahoma', 'Arial', sans-serif;
}

/* تنظیمات برای کدها و بلوک‌های کد - چپ‌چین */
code, pre {
    direction: ltr;
    text-align: left;
    font-family: 'Consolas', 'Monaco', 'Courier New', monospace;
}

/* تنظیمات برای بلوک‌های کد */
.highlight, .codehilite {
    direction: ltr;
    text-align: left;
}

/* تنظیمات برای کدهای inline */
code {
    direction: ltr;
    text-align: left;
    display: inline-block;
}

/* تنظیمات برای imports و کدهای Python */
pre code {
    direction: ltr;
    text-align: left;
    display: block;
}

</style>

<h1 style="font-size: 3em; font-weight: bold; text-align: center; color:rgba(51, 198, 41, 0.49)">
🌿 جزوه کامل برای یادگیری SQLAlchemy 🌿
</h1>


## 📘 **مقدمه**

در این جزوه، با تکیه بر [**مستندات رسمی SQLAlchemy**](https://docs.sqlalchemy.org/en/20/) و همچنین کمک گرفتن از  **هوش مصنوعی‌های مختلف**، تلاش می‌کنم کاربردها و جزئیات مهم این کتابخانه را بررسی کنم.  
هدف این است که مفاهیم را نه‌تنها در بستر **پایتون**، بلکه در ارتباط با  **زبان‌ها و فریم‌ورک‌های مختلف** هم مرور کنیم تا یادگیری جنبه‌ی کاربردی‌تر و گسترده‌تری داشته باشد.



## 🗂️ <span style="color:#FF8C00">فهرست مطالب</span>

**[مبانی و مقدمات](#مبانی-و-مقدمات)**
  - [معرفی SQLAlchemy](#معرفی-sqlalchemy)
    - [SQLAlchemy چیست؟](#sqlalchemy-چیست؟)
    - [مزایا و کاربردها](#مزایا-و-کاربردها)
    - [نصب و راه‌اندازی](#نصب-و-راه‌اندازی)
    - [Core vs ORM](#core-vs-orm)
  - [اتصال به پایگاه داده](#اتصال-به-پایگاه-داده)
    - [Engine و Connection](#engine-و-connection)
    - [Connection Strings](#connection-strings)
    - [Connection Pooling](#connection-pooling)
    - [Database Events](#database-events)

**[SQLAlchemy Core](#sqlalchemy-core)**
  - [Table Definition و MetaData](#table-definition-و-metadata)
    - [Table objects](#table-objects)
    - [Column types](#column-types)
    - [Constraints](#constraints)
    - [Indexes](#indexes)
    - [Schema operations](#schema-operations)
  - [SQL Expression Language](#sql-expression-language)
    - [Select statements](#select-statements)
    - [Insert, Update, Delete](#insert-update-delete)
    - [Joins](#joins)
    - [Functions و Operators](#functions-و-operators)
    - [Subqueries](#subqueries)
  - [Executing Statements](#executing-statements)
    - [Connection execution](#connection-execution)
    - [Result objects](#result-objects)
    - [Transactions](#transactions)

**[SQLAlchemy ORM](#sqlalchemy-orm)**
  - [Declarative Base](#declarative-base)
    - [Model definition](#model-definition)
    - [Table mapping](#table-mapping)
    - [Primary keys](#primary-keys)
    - [Column options](#column-options)
  - [Sessions](#sessions)
    - [Session lifecycle](#session-lifecycle)
    - [Creating و configuring sessions](#creating-و-configuring-sessions)
    - [Session states](#session-states)
    - [Committing و rollback](#committing-و-rollback)
  - [Basic Queries](#basic-queries)
    - [Query objects](#query-objects)
    - [Filtering](#filtering)
    - [Ordering](#ordering)
    - [Limiting](#limiting)

**[Relationships و Advanced ORM](#relationships-و-advanced-orm)**
  - [Relationships](#relationships)
    - [One-to-Many](#one-to-many)
    - [Many-to-One](#many-to-one)
    - [One-to-One](#one-to-one)
    - [Many-to-Many](#many-to-many)
    - [Back references](#back-references)
  - [Lazy Loading vs Eager Loading](#lazy-loading-vs-eager-loading)
    - [Lazy loading patterns](#lazy-loading-patterns)
    - [Eager loading (joinedload, selectinload)](#eager-loading-joinedload-selectinload)
    - [N+1 problem](#n1-problem)
    - [Loading strategies](#loading-strategies)
  - [Advanced Querying](#advanced-querying)
    - [Complex joins](#complex-joins)
    - [Subqueries](#subqueries-1)
    - [Union operations](#union-operations)
    - [Window functions](#window-functions)
    - [Raw SQL integration](#raw-sql-integration)

**[Advanced Topics](#advanced-topics)**
  - [Session Management Patterns](#session-management-patterns)
    - [Session per request](#session-per-request)
    - [Contextual sessions](#contextual-sessions)
    - [Thread-local sessions](#thread-local-sessions)
    - [Session events](#session-events)
  - [Advanced Relationships](#advanced-relationships)
    - [Self-referential relationships](#self-referential-relationships)
    - [Polymorphic relationships](#polymorphic-relationships)
    - [Hybrid properties](#hybrid-properties)
  - [Customization و Extensions](#customization-و-extensions)
    - [Custom types](#custom-types)
    - [Validators](#validators)
    - [Events و listeners](#events-و-listeners)
    - [Mixins](#mixins)
    - [Custom loading techniques](#custom-loading-techniques)

**[Performance و Optimization](#performance-و-optimization)**
  - [Performance Tuning](#performance-tuning)
    - [Query optimization](#query-optimization)
    - [Index strategies](#index-strategies)
    - [Connection pooling](#connection-pooling-1)
    - [Bulk operations](#bulk-operations)
  - [Caching](#caching)
    - [Query result caching](#query-result-caching)
    - [Second-level cache](#second-level-cache)
    - [Dogpile.cache integration](#dogpilecache-integration)

**[Advanced Features](#advanced-features)**
  - [Migrations با Alembic](#migrations-با-alembic)
    - [Migration basics](#migration-basics)
    - [Auto-generating migrations](#auto-generating-migrations)
    - [Manual migrations](#manual-migrations)
    - [Branching و merging](#branching-و-merging)
  - [Testing](#testing)
    - [Testing patterns](#testing-patterns)
    - [Fixtures](#fixtures)
    - [Mock strategies](#mock-strategies)
    - [Database testing](#database-testing)

**[Real-world Applications](#real-world-applications)**
  - [Design Patterns](#design-patterns)
    - [Repository pattern](#repository-pattern)
    - [Unit of Work](#unit-of-work)
    - [Data Mapper](#data-mapper)
    - [Active Record considerations](#active-record-considerations)
  - [Integration](#integration)
    - [Web framework integration (Flask, FastAPI)](#web-framework-integration-flask-fastapi)
    - [Async SQLAlchemy](#async-sqlalchemy)
    - [Multi-database setups](#multi-database-setups)
    - [Sharding strategies](#sharding-strategies)

---

## <span style="color:#FF8C00">مبانی و مقدمات</span>

### <span style="color:#FFB366">معرفی SQLAlchemy</span>

#### <span style="color:#FFCC99">SQLAlchemy چیست؟ </span>
**SQLAlchemy** یکی از قدرتمندترین و محبوب‌ترین کتابخانه‌های **Python** برای کار با پایگاه‌های داده است.  

این کتابخانه دو رویکرد اصلی ارائه می‌دهد:  

- **SQL Toolkit** ← برای نوشتن و اجرای کوئری‌های SQL با امکانات بیشتر و سطح پایین‌تر. 
- **ORM (Object Relational Mapper)** ← برای کار با پایگاه‌های داده از طریق **Python objects** به جای نوشتن مستقیم SQL خام. 

#### <span style="color:#FFCC99">مزایا و کاربردها</span>

#### 1. انتزاع بالا

```python
# به جای نوشتن SQL خام:
cursor.execute("SELECT * FROM users WHERE age > 18")

# می‌توانید بنویسید:
users = session.query(User).filter(User.age > 18).all()
```

#### 2. پشتیبانی از چندین پایگاه داده

- PostgreSQL
- MySQL
- SQLite
- Oracle
- Microsoft SQL Server
- و بسیاری دیگر

#### 3. Type Safety و IntelliSense

- **Type Safety**: وقتی داری کد می‌نویسی، کامپیوتر کمک می‌کنه که نوع داده‌ها درست باشه و جلوی اشتباهات رایج رو بگیره
- **IntelliSense**: این قابلیت IDE هاست که وقتی داری کد می‌نویسی، خودکار پیشنهادها، اتوماتیک تکمیل، و مستندات کوتاه نشون بده

#### 4. Migration Management

مدیریت تغییرات دیتابیس وقتی مدل‌ها رو تغییر میدی.

---

#### <span style="color:#FFCC99">نصب و راه‌اندازی</span>

### نصب پایه

برای نصب SQLAlchemy به صورت پایه:

```bash
pip install sqlalchemy
```

برای نصب با پشتیبانی از **async**:

```bash
pip install "sqlalchemy[asyncio]"
```

### نصب درایورهای پایگاه داده

* **PostgreSQL**:

```bash
pip install psycopg2-binary
```

* **MySQL**:

```bash
pip install pymysql
```

* **Oracle**:

```bash
pip install cx_Oracle
```

---

## نصب برای فریمورک‌های مختلف

* **Flask**:

```bash
pip install flask flask-sqlalchemy flask-migrate
```

* **FastAPI**:

```bash
pip install fastapi sqlalchemy alembic uvicorn
```

* **Django**:
  Django به صورت پیش‌فرض ORM داخلی دارد، اما در صورت نیاز می‌توانید SQLAlchemy را هم استفاده کنید:

```bash
pip install django sqlalchemy
```

---

## تست نصب

برای اطمینان از نصب صحیح، این کد را اجرا کنید:

```python
import sqlalchemy
print(sqlalchemy.__version__)  # باید ورژن نصب شده را نمایش دهد
```


---

#### <span style="color:#FFCC99">Core vs ORM</span>

**execute** متدی است که یک دستور SQL (مثل select, insert, update, delete) را روی پایگاه داده اجرا می‌کند.

SQLAlchemy دو رویکرد اصلی ارائه می‌دهد:

### SQLAlchemy Core (سطح پایین)

Core برای کسانی است که می‌خواهند کنترل بیشتری روی SQL داشته باشند.

```python
from sqlalchemy import create_engine, MetaData, Table, Column, Integer, String, select

# تعریف جدول
metadata = MetaData()
users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String(50)),
    Column('email', String(100))
)

# اتصال و ایجاد جدول
engine = create_engine("sqlite:///example.db")
metadata.create_all(engine)

# کوئری
with engine.connect() as conn:
    # Insert
    conn.execute(users.insert().values(name='احمد', email='ahmad@example.com'))
    
    # Select
    result = conn.execute(select(users).where(users.c.name == 'احمد'))
    for row in result:
        print(f"ID: {row.id}, Name: {row.name}")
```

#### مزایای Core:

- سرعت بیشتر
- کنترل کامل روی SQL
- مناسب برای کوئری‌های پیچیده
- حجم حافظه کمتر

### SQLAlchemy ORM (سطح بالا)

ORM برای توسعه‌دهندگانی است که می‌خواهند با objects Python کار کنند.

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

Base = declarative_base()

# تعریف مدل
class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(100))
    
    def __repr__(self):
        return f"<User(name='{self.name}', email='{self.email}')>"

# راه‌اندازی
engine = create_engine("sqlite:///example.db")
Base.metadata.create_all(engine)
Session = sessionmaker(bind=engine)
session = Session()

# استفاده
# Insert
new_user = User(name='احمد', email='ahmad@example.com')
session.add(new_user)
session.commit()

# Select
users = session.query(User).filter(User.name == 'احمد').all()
for user in users:
    print(user)
```

#### مزایای ORM:

- کد قابل خوانش‌تر
- Type safety
- Relationship handling آسان
- کمتر SQL نوشتن


### <span style="color:#FFB366">اتصال به پایگاه داده</span>

#### <span style="color:#FFCC99">Engine و Connection</span>

**Engine** چیست؟ **Engine** در SQLAlchemy مانند مدیر ارتباط با پایگاه داده عمل می‌کند.  
- یک بار ساخته می‌شود و در تمام برنامه استفاده می‌شود.  
- مسئول مدیریت ارتباطات و اجرای دستورات SQL است.

### ساخت Engine

```python
from sqlalchemy import create_engine

# SQLite
engine = create_engine("sqlite:///myapp.db")

# PostgreSQL
engine = create_engine("postgresql://user:password@localhost/dbname")
```

### استفاده از Connection

#### روش 1: با Context Manager (بهترین روش)

```python
with engine.connect() as conn:
    result = conn.execute("SELECT 1")
    print(result.fetchone())
```

✅ مزیت: بعد از پایان بلوک، ارتباط به‌صورت خودکار بسته می‌شود.

#### روش 2: دستی (باید خودتان close کنید)

```python
conn = engine.connect()
result = conn.execute("SELECT 1")
print(result.fetchone())
conn.close()  # حتماً ارتباط را ببندید
```

---

### مثال در Flask

```python
from flask import Flask
from sqlalchemy import create_engine

app = Flask(__name__)
engine = create_engine("sqlite:///app.db")

@app.route("/test")
def test_db():
    with engine.connect() as conn:
        result = conn.execute("SELECT COUNT(*) FROM users")
        return f"تعداد کاربران: {result.scalar()}"
```



#### <span style="color:#FFCC99">Connection Strings</span>

Connection String آدرس پایگاه داده شماست:

انواع مختلف:

```python
# SQLite
"sqlite:///path/to/database.db"
"sqlite:///C:/path/to/database.db"  # Windows
"sqlite:///:memory:"  # در حافظه

# PostgreSQL  
"postgresql://username:password@localhost:5432/dbname"
"postgresql+psycopg2://user:pass@localhost/dbname"

# MySQL
"mysql://username:password@localhost:3306/dbname"
"mysql+pymysql://user:pass@localhost/dbname"

# SQL Server
"mssql+pyodbc://user:pass@server/dbname?driver=ODBC+Driver+17+for+SQL+Server"
```

#### <span style="color:#FFCC99">Connection Pooling</span>

Pool یعنی استخر اتصال - تعدادی connection آماده نگه می‌دارد.

```python
# تنظیمات Pool
engine = create_engine(
    "postgresql://user:pass@localhost/db",
    pool_size=10,        # 10 تا connection
    max_overflow=20,     # حداکثر 20 تا اضافی
    pool_timeout=30,     # 30 ثانیه صبر
    pool_recycle=3600    # هر ساعت connection ها را reset کن
)

# چک کردن وضعیت Pool
print(f"Pool size: {engine.pool.size()}")
print(f"Active connections: {engine.pool.checked_in()}")
```

#### <span style="color:#FFCC99">Database Events</span>

در SQLAlchemy، Eventها مکانیزمی هستند که به توسعه‌دهنده اجازه می‌دهد به رویدادها و مراحل مختلف عملیات دیتابیس گوش دهد و به آن‌ها واکنش نشان دهد. این قابلیت امکان مانیتورینگ، لاگینگ و اعمال تغییرات سفارشی در سطح اتصال، کوئری یا تراکنش را فراهم می‌کند.

```python
# قبل از اتصال
@event.listens_for(engine, "connect")
def set_sqlite_pragma(dbapi_connection, connection_record):
    if "sqlite" in str(engine.url):
        cursor = dbapi_connection.cursor()
        cursor.execute("PRAGMA foreign_keys=ON")
        cursor.close()

# قبل از execute شدن کوئری
@event.listens_for(engine, "before_cursor_execute")
def receive_before_cursor_execute(conn, cursor, statement, parameters, context, executemany):
    print(f"اجرا می‌شود: {statement}")
```

---


## <span style="color:#FF8C00">SQLAlchemy Core</span>

### <span style="color:#FFB366">Table Definition و MetaData</span>

- **MetaData** یک شیء مرکزی است که تمام اطلاعات مربوط به جداول، ستون‌ها و ارتباطات پایگاه داده را نگه‌داری و مدیریت می‌کند.

- یعنی هر جدول (Table) که تعریف می‌کنی معمولاً به یک **MetaData** وصل می‌شود تا بعداً بتوان همه آن‌ها را با هم ایجاد، حذف یا مدیریت کرد.

#### <span style="color:#FFCC99">Table objects</span>

Table در SQLAlchemy مثل نقشه جدول شماست.

```python
from sqlalchemy import MetaData, Table, Column, Integer, String, DateTime
from datetime import datetime

metadata = MetaData()

# تعریف جدول users
users_table = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String(50), nullable=False),
    Column('email', String(100), unique=True),
    Column('created_at', DateTime, default=datetime.utcnow)
)

# ایجاد جدول
engine = create_engine("sqlite:///example.db")
metadata.create_all(engine)
```

#### <span style="color:#FFCC99">Column types</span>

انواع اصلی Column:

```python
from sqlalchemy import Integer, String, Text, Boolean, DateTime, Float, Numeric

users = Table('users', metadata,
    # اعداد
    Column('id', Integer),
    Column('age', Integer),
    Column('salary', Float),
    Column('balance', Numeric(10, 2)),  # 10 رقم، 2 اعشار
    
    # متن
    Column('name', String(50)),         # حداکثر 50 کاراکتر
    Column('bio', Text),                # متن طولانی
    
    # تاریخ و زمان  
    Column('created_at', DateTime),
    Column('birth_date', DateTime),
    
    # True/False
    Column('is_active', Boolean, default=True)
)
```

در FastAPI/Flask:

```python
# Flask-SQLAlchemy
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(50), nullable=False)
    email = db.Column(db.String(100), unique=True)
    is_active = db.Column(db.Boolean, default=True)

# FastAPI
from sqlalchemy import Column, Integer, String, Boolean
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    is_active = Column(Boolean, default=True)
```

#### <span style="color:#FFCC99">Constraints</span>

انواع Constraint:

```python
from sqlalchemy import ForeignKey, CheckConstraint, UniqueConstraint

users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('name', String(50), nullable=False),
    Column('email', String(100), unique=True),
    Column('age', Integer),
    
    # Check constraint
    CheckConstraint('age >= 18', name='age_check'),
    
    # Unique constraint
    UniqueConstraint('email', 'name', name='unique_email_name')
)

# جدول orders با Foreign Key
orders = Table('orders', metadata,
    Column('id', Integer, primary_key=True),
    Column('user_id', Integer, ForeignKey('users.id')),
    Column('total', Float)
)
```

#### <span style="color:#FFCC99">Indexes</span>

Index برای سرعت بخشیدن جستجو:

```python
from sqlalchemy import Index

users = Table('users', metadata,
    Column('id', Integer, primary_key=True),
    Column('email', String(100)),
    Column('city', String(50)),
    Column('age', Integer),
    
    # Index ساده
    Index('idx_email', 'email'),
    
    # Composite Index
    Index('idx_city_age', 'city', 'age'),
    
    # Unique Index
    Index('idx_email_unique', 'email', unique=True)
)
```

#### <span style="color:#FFCC99">Schema operations</span>

ایجاد و حذف:

```python
# ایجاد همه جداول
metadata.create_all(engine)

# ایجاد فقط یک جدول
users_table.create(engine)

# حذف همه جداول
metadata.drop_all(engine)

# حذف یک جدول
users_table.drop(engine)
```

---


### <span style="color:#FFB366">SQL Expression Language</span>

فرض می‌کنیم یک جدول به اسم users_table داریم با ستون‌های: id, name, email, age, is_active
و جدول orders_table با ستون‌های: id, user_id, total
#### <span style="color:#FFCC99">Select statements</span>

دستورات SELECT در SQLAlchemy برای انتخاب و بازیابی داده‌ها از جداول استفاده می‌شوند.

**انتخاب همه ردیف‌ها**

```python
from sqlalchemy import select

stmt = select(users_table) # انتخاب همه ردیف ها
with engine.connect() as conn:
    result = conn.execute(stmt)
    for row in result:
        print(f"نام: {row.name}، ایمیل: {row.email}")
```

**انتخاب ستون خاص**

```python
stmt = select(users_table.c.name, users_table.c.email)
# c یعنی ستون
```

**با شرط ساده**

```python
stmt = select(users_table).where(users_table.c.age > 25)
```

**چند شرط با AND**

```python
stmt = select(users_table).where(
    (users_table.c.age > 18) & (users_table.c.is_active == True)
)
```

**شرط LIKE**

```python
stmt = select(users_table).where(users_table.c.name.like('احمد%'))
```

#### <span style="color:#FFCC99">Insert, Update, Delete</span>

**Insert – اضافه کردن داده**

```python
# Insert یکی
stmt = users_table.insert().values(name='علی', email='ali@test.com')
with engine.connect() as conn:
    result = conn.execute(stmt)
    print(f"ID جدید: {result.inserted_primary_key}")

# Insert چندتایی
stmt = users_table.insert()
with engine.connect() as conn:
    conn.execute(stmt, [
        {'name': 'احمد', 'email': 'ahmad@test.com'},
        {'name': 'فاطمه', 'email': 'fateme@test.com'}
    ])
```

**Update – به‌روزرسانی**

```python
stmt = users_table.update().where(users_table.c.id == 1).values(name='علی احمدی')

with engine.connect() as conn:
    result = conn.execute(stmt)
    print(f"{result.rowcount} رکورد به‌روزرسانی شد")
```

**Delete – حذف**

```python
stmt = users_table.delete().where(users_table.c.age < 18)

with engine.connect() as conn:
    result = conn.execute(stmt)
    print(f"{result.rowcount} رکورد حذف شد")
```

#### <span style="color:#FFCC99">Joins</span>

Joinها برای ادغام داده‌ها از دو یا چند جدول بر اساس یک شرط مشترک کاربرد دارند.

1️⃣ Inner Join

داده‌ها را فقط زمانی برمی‌گرداند که ردیف‌های هر دو جدول با شرط join مطابقت داشته باشند.

مثال کاربردی: گرفتن فقط کاربرانی که حداقل یک سفارش ثبت کرده‌اند.

```python
# Inner Join
stmt = select(users_table.c.name, orders_table.c.total).join(
    orders_table, users_table.c.id == orders_table.c.user_id
)
```

**مفهوم ساده:**

می‌خوای اطلاعات کاربر و مجموع سفارشش رو بگیری.

Inner Join یعنی فقط کاربرانی که حداقل یک سفارش دارند نمایش داده می‌شوند.

شرط `users_table.c.id == orders_table.c.user_id` مشخص می‌کنه کدام کاربر به کدام سفارش وصل شود.

💡 **نتیجه:** کاربرانی بدون سفارش نمایش داده نمی‌شوند.

2️⃣ Outer Join (Left Join)

همه ردیف‌های جدول اصلی (چپ) را برمی‌گرداند، حتی اگر مطابقتی در جدول دوم وجود نداشته باشد.

مثال کاربردی: گرفتن همه کاربران، حتی آن‌هایی که هنوز هیچ سفارشی ثبت نکرده‌اند؛ در این صورت ستون‌های جدول دوم (orders) مقدار NULL دارند.

```python
# Left (Outer) Join
stmt = select(users_table.c.name, orders_table.c.total).select_from(
    users_table.outerjoin(orders_table)
)
```

**مفهوم ساده:**

باز هم می‌خوای اطلاعات کاربر و مجموع سفارشش رو بگیری.

Left Outer Join یعنی همه کاربران نمایش داده می‌شوند، حتی اگر هیچ سفارشی نداشته باشند.

ستون‌های سفارش برای کاربرانی که سفارش ندارند، مقدار NULL خواهند داشت.

💡 **نتیجه:** هیچ کاربری حذف نمی‌شود، حتی بدون سفارش.

🔹 **مفهوم .c**

.c یعنی ستون‌های جدول (columns).

وقتی می‌نویسی users_table.c.name یعنی ستون name از جدول users_table.

#### <span style="color:#FFCC99">Functions و Operators</span>

**Functions – توابع SQL**

مثال‌های کاربردی:

```python
from sqlalchemy import select, func

# تعداد کاربران
stmt = select(func.count(users_table.c.id))

# بیشینه، کمینه و میانگین سن کاربران
stmt = select(
    func.max(users_table.c.age),
    func.min(users_table.c.age), 
    func.avg(users_table.c.age)
)

# گروه‌بندی بر اساس شهر و تعداد کاربران
stmt = select(
    users_table.c.city,
    func.count(users_table.c.id)
).group_by(users_table.c.city)
```

💡 **نکته:**

- `func` معادل توابع SQL است
- می‌توانی از توابع aggregation مثل COUNT, MAX, MIN, AVG, SUM استفاده کنی
- aggregation توابعی است که برای ترکیب یا تجزیه داده‌ها از جدول استفاده می‌شوند.

**Operators – عملگرها**

*مقایسه:*

```python
users_table.c.age > 18
users_table.c.name == 'علی'
users_table.c.email.like('%gmail%')
users_table.c.id.in_([1, 2, 3])
```

*عملگرهای منطقی:*

```python
# AND
(users_table.c.age > 18) & (users_table.c.is_active == True)

# OR
(users_table.c.city == 'تهران') | (users_table.c.city == 'اصفهان')
```

💡 **نکته:**

- `|` = OR
- `&` = AND
- `like()` برای جستجوی شبیه‌سازی رشته استفاده می‌شود
- `in_()` بررسی عضویت در یک لیست


#### <span style="color:#FFCC99">Subqueries</span>

**Subquery ساده**

```python
# کاربرانی که حداقل یک سفارش دارند
subq = select(orders_table.c.user_id).distinct()
stmt = select(users_table).where(users_table.c.id.in_(subq))
```

**Subquery با alias و scalar**

```python
subq = select(func.avg(users_table.c.age)).scalar_subquery()
stmt = select(users_table).where(users_table.c.age > subq)
```

**EXISTS**

```python
from sqlalchemy import exists

stmt = select(users_table).where(
    exists().where(orders_table.c.user_id == users_table.c.id)
)
```

💡 **نکته:**

- **Subquery** = کوئری داخلی
- **scalar_subquery()** = بازگرداندن یک مقدار تکی
- **exists()** = بررسی وجود حداقل یک ردیف

---


### <span style="color:#FFB366">Executing Statements</span>

#### <span style="color:#FFCC99">Connection execution</span>

روش‌های اجرا
```python
from sqlalchemy import create_engine, text, select

engine = create_engine("sqlite:///example.db")

# روش ۱: با Connection
with engine.connect() as conn:
    result = conn.execute(text("SELECT * FROM users"))
    print(result.fetchall())

# روش ۲: مستقیم از Engine
result = engine.execute("SELECT COUNT(*) FROM users")
print(result.scalar())

# روش ۳: با Statement Object (مدرن‌تر و امن‌تر)
stmt = select(users_table).where(users_table.c.age > 25)
with engine.connect() as conn:
    result = conn.execute(stmt)
    for row in result:
        print(f"نام: {row.name}")
```

پارامترگذاری (Parameterized Queries)
```python
with engine.connect() as conn:
    # یک پارامتر
    result = conn.execute(
        text("SELECT * FROM users WHERE age > :min_age"),
        {"min_age": 18}
    )

    # چند پارامتر
    result = conn.execute(
        text("SELECT * FROM users WHERE age BETWEEN :min_age AND :max_age"),
        {"min_age": 18, "max_age": 65}
    )
```


💡 مزیت: امنیت بیشتر (SQL Injection جلوگیری میشه)

#### <span style="color:#FFCC99">Result objects</span>

گرفتن داده‌ها
```python
stmt = select(users_table)
with engine.connect() as conn:
    result = conn.execute(stmt)
    
    # یک سطر
    first_row = result.fetchone()
    print(f"اولین کاربر: {first_row.name}")

    # چند سطر
    some_rows = result.fetchmany(5)

    # همه سطرها
    all_rows = result.fetchall()
```


#### <span style="color:#FFCC99">Transactions</span>

📌 تراکنش = مجموعه‌ای از عملیات که یا همه انجام میشه یا هیچ‌کدوم.

ساده (خودکار)
```python
with engine.connect() as conn:
    conn.execute(users_table.insert().values(name="احمد"))
    conn.execute(users_table.insert().values(name="علی"))
    # در پایان بلوک with → commit خودکار
```

توضیح:

اینجا وقتی with تمام میشه، SQLAlchemy به‌طور خودکار یک transaction باز کرده بود و اون رو commit می‌کنه.

اگر در وسط اجرای کوئری‌ها خطایی رخ بده، تراکنش به صورت خودکار rollback میشه.

یعنی تمام کوئری‌هایی که داخل بلوک with اجرا شدن یا همه ذخیره میشن یا هیچ‌کدوم.

✅ پس این حالت اتمیک هست.

دستی
```python
conn = engine.connect()
trans = conn.begin()
try:
    conn.execute(users_table.insert().values(name="احمد"))
    conn.execute(users_table.insert().values(name="علی"))
    trans.commit()  # ذخیره تغییرات
except:
    trans.rollback()  # برگرداندن
finally:
    conn.close()
```

توضیح:

اینجا خودت به صورت دستی یک transaction باز می‌کنی (conn.begin()).

بعد از اجرای کوئری‌ها، باید خودت commit() یا rollback() بزنی.

این روش وقتی لازمه که کنترل کامل روی تراکنش داشته باشی (مثلاً وسط کار شرط خاصی بررسی کنی و تصمیم بگیری commit بشه یا rollback).

✅ این حالت هم اتمیک هست، چون اگر commit نشه، همه تغییرات rollback میشن.

---
🔹 خلاصه:

Connection ← برای اجرای کوئری

Result ← برای گرفتن خروجی و کار با سطرها

Transaction ← برای اطمینان از یکپارچگی داده‌ها

---

## <span style="color:#FF8C00">SQLAlchemy ORM</span>

### <span style="color:#FFB366">Declarative Base</span>

🔹 Declarative Base چیست؟

یک روش شیءگرا برای تعریف جدول‌هاست.

به‌جای اینکه به‌صورت دستی Table بسازید، یک کلاس پایتون می‌نویسید و SQLAlchemy خودش آن را به جدول دیتابیس متصل (Map) می‌کند.

در SQLAlchemy ما دو راه برای تعریف جدول داریم:

روش دستی (Table-based): با استفاده از Table و ستون‌ها (Column) جدول می‌سازیم.

روش شیءگرا (Declarative Base): با استفاده از کلاس‌های پایتون جدول‌ها را تعریف می‌کنیم.

#### <span style="color:#FFCC99">Model definition</span>


**روش قدیمی (SQLAlchemy < 2.0)**
```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

# پایه
Base = declarative_base()

# تعریف مدل
class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    email = Column(String(100))
```


➡️ این کد یک جدول به اسم users در دیتابیس می‌سازه.
هر شیء از کلاس User معادل یک رکورد (سطر) در جدول هست.

**روش جدید (SQLAlchemy 2.0)**
```python
from sqlalchemy.orm import DeclarativeBase, Mapped, mapped_column

class Base(DeclarativeBase):
    pass

class User(Base):
    __tablename__ = "users"
    
    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(50))
    email: Mapped[str] = mapped_column(String(100))
```


✔️ فرقش اینه که در نسخه ۲.۰، تایپ‌ها (Mapped[int]) واضح‌تر و سازگارتر با پایتون مدرن تعریف شدن.

#### <span style="color:#FFCC99">Table mapping</span>

Table Mapping = وصل کردن یک کلاس پایتون به یک جدول دیتابیس

🔹 حالت ساده (اسم‌ها یکسان)

وقتی اسم جدول و ستون‌ها همون اسم کلاس و ویژگی‌ها باشه، کار خیلی ساده‌ست:

```python
class User(Base):
    __tablename__ = 'users'   # جدول دیتابیس

    id = Column(Integer, primary_key=True)  # ستون id
    name = Column(String(50))               # ستون name
```


اینجا کلاس User به جدول users وصل شده.

ویژگی id در پایتون دقیقاً به ستون id در دیتابیس وصل میشه.

ویژگی name در پایتون دقیقاً به ستون name در دیتابیس وصل میشه.

📌 یعنی اسم‌ها یکی هستن ← نگاشت خودکار و مستقیم.

🔹 حالت سفارشی (اسم‌ها فرق کنن)

گاهی توی دیتابیس اسم ستون‌ها یا جدول یه چیز دیگه‌ست، اما نمی‌خوای توی پایتون از همون اسم سخت استفاده کنی.
اینجا Mapping سفارشی کمک می‌کنه:

```python
class User(Base):
    __tablename__ = 'user_accounts'   # جدول دیتابیس اسمش user_accounts است

    user_id = Column("id", Integer, primary_key=True)     # ستون id → ویژگی user_id
    full_name = Column("name", String(100))               # ستون name → ویژگی full_name
```


جدول واقعی دیتابیس اسمش user_accounts هست.

در دیتابیس ستونی به اسم id داریم، ولی در پایتون اسمش رو user_id گذاشتیم.

در دیتابیس ستونی به اسم name داریم، ولی در پایتون از full_name استفاده می‌کنیم.

📌 اینطوری کد پایتون خواناتر میشه، اما همچنان به دیتابیس وصل میشه.

#### <span style="color:#FFCC99">Primary keys</span>

**ساده**
```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)  # Auto increment
```

**با UUID**
```python
import uuid
from sqlalchemy.dialects.postgresql import UUID

class User(Base):
    __tablename__ = "users"
    id = Column(UUID(as_uuid=True), primary_key=True, default=uuid.uuid4)
```

**ترکیبی (Composite Key)**
```python
class OrderItem(Base):
    __tablename__ = "order_items"
    order_id = Column(Integer, primary_key=True)
    product_id = Column(Integer, primary_key=True)
    quantity = Column(Integer)
```

#### <span style="color:#FFCC99">Column options</span>

```python
from sqlalchemy import Boolean, DateTime
from datetime import datetime

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True)
    name = Column(String(50), nullable=False)   # اجباری
    email = Column(String(100), unique=True)    # باید یکتا باشه
    is_active = Column(Boolean, default=True)   # مقدار پیش‌فرض
    created_at = Column(DateTime, default=datetime.utcnow)  # زمان ساخت
    updated_at = Column(DateTime, onupdate=datetime.utcnow) # زمان تغییر
    city = Column(String(50), index=True)       # ایندکس
    status = Column(String(20), server_default="active") # پیش‌فرض سمت سرور
```


### <span style="color:#FFB366">Sessions</span>

🟢 Session چیست؟

یک پل ارتباطی بین کد پایتون و دیتابیسه.

یعنی همهٔ کارهای ORM (افزودن، تغییر، حذف، خواندن) از طریق Session انجام میشه.

Session تغییرات رو نگه می‌داره تا وقتی که commit() بزنی در دیتابیس ثبت بشن.

📌 پس Session مثل یک دفترچه یادداشت موقت هست که در آخر می‌تونی تصمیم بگیری تغییرات رو ذخیره کنی یا پاک کنی.

این Session در SQLAlchemy را با Session احراز هویت اشتباه نگیرید؛ در ادامه توضیح داده می‌شود.

#### <span style="color:#FFCC99">Session lifecycle</span>

🔹 چرخهٔ Session (Session Lifecycle)

**ایجاد Session Factory**

```python
from sqlalchemy.orm import sessionmaker

Session = sessionmaker(bind=engine)
```

این یعنی "کارخانه"‌ی ساخت Session.

**ایجاد Session**

```python
session = Session()
```

**استفاده از Session**

```python
user = User(name="احمد")
session.add(user)
```

**Commit (ذخیره در دیتابیس)**

```python
session.commit()
```

**بستن Session**

```python
session.close()
```

#### <span style="color:#FFCC99">Creating و configuring sessions</span>

```python
Session = sessionmaker(
    bind=engine,
    autoflush=False,        # خودش قبل از query تغییرات رو flush نکنه
    autocommit=False,       # خودش commit نکنه
    expire_on_commit=False  # بعد از commit داده‌ها باطل نشن
)
```
📌 معمولاً در فریم‌ورک‌ها این تنظیمات رو ست می‌کنن تا کنترل بیشتری داشته باشی.

#### <span style="color:#FFCC99">Session states</span>

```python
session = Session()

# 1. Transient (بی‌ارتباط)
user = User(name="احمد")

# 2. Pending (در انتظار)
session.add(user)
print(user in session.new)  # True

# 3. Persistent (ثابت)
session.commit()
print(user in session)  # True
print(user.id)  # حالا ID دارد

# 4. Detached (جدا شده)
session.expunge(user)  # حذف از session
print(user in session)  # False

# 5. Deleted (حذف شده)
session.delete(user)
print(user in session.deleted)  # True
```

#### <span style="color:#FFCC99">Committing و rollback</span>

Commit: ذخیره کردن تغییرات در دیتابیس.

Rollback: برگرداندن همه تغییرات (اگر خطا پیش اومده باشه).

مثال:

```python
session = Session()
try:
    user1 = User(name="احمد")
    user2 = User(name="علی")
    session.add_all([user1, user2])
    session.commit()
except:
    session.rollback()
finally:
    session.close()
```

🔹 **استفاده از Context Manager (روش پیشنهادی)**
```python
with Session() as session:
    user = User(name="احمد")
    session.add(user)
    session.commit()
```


📌 اینطوری Session خودش در پایان بسته میشه.

نکات پایانی:
1️⃣ Session در SQLAlchemy / ORM

کاربرد: مدیریت ارتباط با دیتابیس و تراکنش‌ها

مسئول ذخیره، ویرایش، حذف، و خواندن داده‌هاست.

کنترل می‌کنه که تغییرات به دیتابیس commit بشن یا rollback.

وضعیت آبجکت‌ها رو نگه می‌داره: Transient, Pending, Persistent, Detached, Deleted

✅ نتیجه: همه عملیات ORM و کوئری‌ها از طریق همین session انجام میشه.

2️⃣ Session در فریم‌ورک‌ها (Flask, FastAPI, Django)

کاربرد: مدیریت کاربر لاگین‌شده و احراز هویت

معمولاً وقتی کاربر وارد میشه، اطلاعاتی مثل user_id یا token توی session ذخیره میشه.

این Session به دیتابیس وصل نیست، بلکه یک Context ذخیره اطلاعات بین درخواست‌ها هست.

در Flask/FastAPI معمولاً با cookie یا server-side session store پیاده میشه.

در Django، session مدیریت شده و اطلاعات داخل دیتابیس یا cache ذخیره میشه.

| نوع Session | SQLAlchemy ORM                    | فریم‌ورک (Flask/FastAPI/Django)   |
| ----------- | --------------------------------- | --------------------------------- |
| هدف         | مدیریت ارتباط با دیتابیس          | مدیریت احراز هویت / اطلاعات کاربر |
| شامل        | Object states, تراکنش‌ها          | user_id, token, login state       |
| طول عمر     | کوتاه‌مدت، معمولا برای هر request | طولانی‌تر، بین request ها         |
| عملیات مهم  | add, commit, rollback, query      | set/get/remove، check login       |
| محل ذخیره   | حافظه پایتون، دیتابیس             | cookie, دیتابیس، cache            |

🔹 نکته کلیدی:

SQLAlchemy Session و Session فریم‌ورک کاملاً مستقل هستند.

می‌تونی همزمان از هر دو استفاده کنی: **SQLAlchemy Session** برای کار با داده‌ها، و فریم‌ورک Session برای مدیریت کاربر.

### <span style="color:#FFB366">Basic Queries</span>

وقتی با Session کار می‌کنی، عملاً داری روی دیتابیس کوئری می‌زنی.
Session بهت امکاناتی میده تا داده‌ها رو بخونی، فیلتر کنی، مرتب کنی و محدود کنی.

#### <span style="color:#FFCC99">Query objects</span>

Query Objects (شیء کوئری)

🔹 وقتی می‌خوای داده‌ها رو بگیری، اول یه Query Object می‌سازی:

```python
session = Session()

# ساخت یک Query برای جدول User
query = session.query(User)

print(type(query))  
# خروجی: <class 'sqlalchemy.orm.query.Query'>
```

این Query Object مثل یه قالب آماده‌ست.
بعد می‌تونی روی اون اجرا کنی:

```python
users = query.all()   # همه User ها
first_user = query.first()  # اولین User
user_count = query.count()  # تعداد کل
one_user = query.one()      # باید دقیقاً یکی باشه
```

#### <span style="color:#FFCC99">Filtering</span>

می‌خوای فقط یه بخشی از داده‌ها رو بگیری؟ از filter یا filter_by استفاده کن.

```python
# همه افراد بالای 18 سال
adult_users = session.query(User).filter(User.age >= 18).all()

# همه کاربران فعال
active_users = session.query(User).filter_by(is_active=True).all()
```

🔹 چند شرط هم می‌تونی بزنی:

```python
query = session.query(User).filter(
    User.age >= 18,
    User.is_active == True,
    User.city == 'تهران'
)
```

📌 اپراتورها:

```python
session.query(User).filter(User.name.like('احمد%'))   # شروع با احمد
session.query(User).filter(User.email.contains('@gmail'))  # شامل @gmail
session.query(User).filter(User.id.in_([1, 2, 3]))    # داخل لیست
session.query(User).filter(User.age.between(18, 65))  # بین 18 و 65
session.query(User).filter(User.phone.is_(None))      # NULL
```

🔹 شرط‌های ترکیبی:

```python
from sqlalchemy import and_, or_, not_

# AND
session.query(User).filter(and_(User.age >= 18, User.is_active == True))

# OR
session.query(User).filter(or_(User.city == 'تهران', User.city == 'اصفهان'))

# NOT
session.query(User).filter(not_(User.is_deleted))
```

#### <span style="color:#FFCC99">Ordering</span>

**مرتب‌سازی (Ordering)**
```python
# صعودی
users = session.query(User).order_by(User.name).all()

# نزولی
users = session.query(User).order_by(User.created_at.desc()).all()

# چند ستون
users = session.query(User).order_by(
    User.city,
    User.name.desc()
).all()
```

📌 پیشرفته‌تر:

```python
from sqlalchemy import func

# بر اساس طول نام
session.query(User).order_by(func.length(User.name))

# تصادفی
session.query(User).order_by(func.random()).limit(5)

# NULL ها آخر بیان
session.query(User).order_by(User.phone.nullslast())
```

#### <span style="color:#FFCC99">Limiting</span>

خیلی وقتا همه داده‌ها رو نمی‌خوای. برای این Pagination داریم:

```python
# فقط 10 رکورد
users = session.query(User).limit(10).all()

# از رکورد 20 تا 30
users = session.query(User).offset(20).limit(10).all()

# آخرین 5 نفر
latest_users = session.query(User)\
    .order_by(User.created_at.desc())\
    .limit(5)\
    .all()
```



## <span style="color:#FF8C00">Relationships و Advanced ORM</span>

### <span style="color:#FFB366">Relationships</span>

وقتی چند جدول داریم، باید بگیم که رابطه بینشون چیه:

- یک کاربر می‌تونه چند سفارش داشته باشه (One-to-Many)

- یک سفارش فقط به یک کاربر تعلق داره (Many-to-One)

- هر کاربر یک پروفایل داره (One-to-One)

- کاربرها می‌تونن نقش‌های مختلف داشته باشن و برعکس (Many-to-Many)

- ForeignKey ← تو دیتابیس میگه این رکورد به کدوم جدول وصله. ستونی که به رکورد جدول دیگه اشاره می‌کنه

- relationship ← تو پایتون بهت اجازه میده راحت به رکوردهای مرتبط دسترسی داشته باشی. این دیگه مخصوص ORM (مثل SQLAlchemy یا Django ORM) هست.
به جای اینکه مدام JOIN بزنی، می‌تونی مستقیم از آبجکت‌ها استفاده کنی.

#### <span style="color:#FFCC99">One-to-Many</span>

یک کاربر می‌تونه چند سفارش داشته باشه.

```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    orders = relationship("Order", back_populates="user")  # لیست سفارش‌ها

class Order(Base):
    __tablename__ = "orders"
    id = Column(Integer, primary_key=True)
    total = Column(Float)
    user_id = Column(Integer, ForeignKey("users.id"))  # این سفارش مال کدوم کاربره؟

    user = relationship("User", back_populates="orders")
```

**استفاده:**

```python
user = session.query(User).first()
print(user.orders)       # لیست سفارش‌ها
```

در جدول Order یک ForeignKey داریم (user_id) ← این اتصال اصلی توی دیتابیسه.

اما ORM (SQLAlchemy) می‌خواد رابطه‌ی دوطرفه بسازه:

از سمت User: دسترسی به لیست سفارش‌ها ← user.orders

از سمت Order: دسترسی به صاحب سفارش ← order.user

اگر فقط یک طرف relationship رو بذاری، از همون سمت کار می‌کنه، ولی معمولا دوطرفه راحت‌تره (یعنی بتونی هم user.orders بزنی هم order.user).

👉 پس: دوتا relationship برای راحتی در کدنویسیه، نه برای تعیین نوع رابطه.
نوع رابطه رو در واقع همون ForeignKey مشخص می‌کنه.

#### <span style="color:#FFCC99">Many-to-One</span>

همون مثال بالاست، فقط از سمت سفارش نگاه می‌کنیم:

```python
order = session.query(Order).first()
print(f"این سفارش برای {order.user.name} است")
```

#### <span style="color:#FFCC99">One-to-One</span>

هر کاربر یک پروفایل داره.

```python
class Profile(Base):
    __tablename__ = "profiles"
    id = Column(Integer, primary_key=True)
    bio = Column(String(200))
    user_id = Column(Integer, ForeignKey("users.id"), unique=True)

    user = relationship("User", back_populates="profile")

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    profile = relationship("Profile", back_populates="user", uselist=False)
```

کلید خارجی (FK) یعنی «این ستون به جدول دیگه وصل میشه».

وقتی unique=True هم بزنی یعنی هر user_id فقط یک بار می‌تونه تو جدول بیاد.

✅ نتیجه:
اینطوری رابطه تبدیل میشه به One-to-One (هر کاربر فقط یک پروفایل می‌تونه داشته باشه).

بدون unique=True میشه One-to-Many (هر کاربر می‌تونه چند پروفایل داشته باشه).

به طور پیش‌فرض relationship فکر می‌کنه ممکنه چندتا آبجکت برگردونه (مثلاً user.orders → یک لیست).

ولی وقتی رابطه یک‌به‌یک (One-to-One) باشه، می‌خوای یه آبجکت تکی برگرده نه لیست.

اینجاست که `uselist=False` استفاده می‌شود.


#### <span style="color:#FFCC99">Many-to-Many</span>

کاربرها می‌تونن چند نقش داشته باشن (ادمین، کاربر ساده).

```python
user_roles = Table(
    "user_roles", Base.metadata,
    Column("user_id", Integer, ForeignKey("users.id")),
    Column("role_id", Integer, ForeignKey("roles.id"))
)

class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    roles = relationship("Role", secondary=user_roles, back_populates="users")

class Role(Base):
    __tablename__ = "roles"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    users = relationship("User", secondary=user_roles, back_populates="roles")
```

این secondary=user_roles در Many-to-Many چیه؟
در رابطه‌ی Many-to-Many باید یک جدول میانی داشته باشیم
در اینجا جدول user_roles مثل پل بین users و roles عمل می‌کنه. 

#### <span style="color:#FFCC99">Back references</span>

🔹 back_populates

باید دو طرف رابطه رو خودت تعریف کنی.

اسم attribute (ویژگی) رو دستی مشخص می‌کنی.

مثال One-to-Many (کاربر ↔ سفارش‌ها):

```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    orders = relationship("Order", back_populates="user")  # سمت User

class Order(Base):
    __tablename__ = "orders"
    id = Column(Integer, primary_key=True)
    total = Column(Float)
    user_id = Column(Integer, ForeignKey("users.id"))

    user = relationship("User", back_populates="orders")  # سمت Order
```


📌 یعنی:

از سمت کاربر: user.orders ← لیست سفارش‌ها

از سمت سفارش: order.user ← کاربر مربوط به اون سفارش

اینجا دو خط relationship داری و باید دقیقاً همدیگه رو اشاره بدن.

🔹 backref

به جای اینکه دو بار تعریف کنی، یک بار تعریف می‌کنی، و sqlalchemy خودش طرف مقابل رو می‌سازه.

یعنی shortcut هست.

مثال همون بالا، اما کوتاه‌تر:

```python
class User(Base):
    __tablename__ = "users"
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

class Order(Base):
    __tablename__ = "orders"
    id = Column(Integer, primary_key=True)
    total = Column(Float)
    user_id = Column(Integer, ForeignKey("users.id"))

    user = relationship("User", backref="orders")
```

📌 حالا هم داری:

```python
order.user
user.orders
```

ولی فقط یک بار relationship نوشتی.

### <span style="color:#FFB366">Lazy Loading vs Eager Loading</span>

#### <span style="color:#FFCC99">Lazy loading patterns</span>

داده‌ها وقت نیاز load می‌شوند:
```python
user = session.query(User).first()  # فقط جدول User کوئری میشه
print(user.name)

# وقتی اینجا دسترسی می‌کنی، تازه orders لود میشه
print(len(user.orders))  
# => حالا یه کوئری جدید زده میشه
```

#### <span style="color:#FFCC99">Eager loading (joinedload, selectinload)</span>

همه داده‌ها یکجا load می‌شوند:

🔹 فرق selectinload و joinedload

- هر دو برای Eager Loading هستن (یعنی داده‌ها رو همون اول میارن)،
ولی روش کارشون فرق می‌کنه:

📍 joinedload

از JOIN در همون کوئری اصلی استفاده می‌کنه.

همه‌چیز با یک کوئری میاد.

سریع‌تره وقتی داده کم باشه.

مشکل: اگه جدول فرزند (مثل orders) خیلی رکورد داشته باشه، داده تکراری زیادی کشیده میشه.

📌 مثال:

```python
users = session.query(User).options(joinedload(User.orders)).all()
# SQL: SELECT users.*, orders.* FROM users LEFT JOIN orders ...
```

📍 selectinload

اول همه User‌ها رو میاره، بعد یه کوئری جدا برای همه ordersها میزنه.

نتیجه: دو کوئری (ولی بهینه).

بهتره وقتی رکوردهای فرزند زیادن.

📌 مثال:

```python
users = session.query(User).options(selectinload(User.orders)).all()
# SQL 1: SELECT * FROM users
# SQL 2: SELECT * FROM orders WHERE user_id IN (list of all ids)
```


✅ پس:

داده کم ← joinedload خوبه.

داده زیاد ← selectinload بهینه‌تره.

#### <span style="color:#FFCC99">N+1 problem</span>

وقتی برای گرفتن یک مجموعه داده، ۱ کوئری اولیه + N کوئری اضافی برای هر رکورد زده بشه.
📌 **مثال (N+1):**

```python
users = session.query(User).all()  # 1 کوئری
for user in users:
    print(len(user.orders))        # N کوئری اضافه (برای هر User جدا)
```

📌 **مثال (Eager Loading):**

```python
users = session.query(User).options(joinedload(User.orders)).all()
for user in users:
    print(len(user.orders))  # کوئری اضافه نمی‌خوره
```

#### <span style="color:#FFCC99">Loading strategies</span>

🔹 Loading Strategies (روش‌های بارگذاری رابطه‌ها)

وقتی relationship تعریف می‌کنی، می‌تونی تعیین کنی چطور داده لود بشه:

1. Lazy (پیش‌فرض: "select")

کوئری فقط وقتی لازم باشه زده میشه.
📌 مثال:

```python
orders = relationship("Order", lazy="select")  
# فقط وقتی user.orders صدا بزنی، کوئری orders اجرا میشه
```

2. Eager همیشه ( "joined" )

همراه موجودیت اصلی (User) با JOIN میاره.
📌 مثال:

```python
orders = relationship("Order", lazy="joined")  
# وقتی User ها رو بگیری، orders هم همزمان میاد
```

3. فقط وقت نیاز ( "dynamic" )

به جای لیست، یه Query object برمی‌گردونه.

می‌تونی روی همون رابطه فیلتر و limit بزنی.

📌 مثال:

```python
orders = relationship("Order", lazy="dynamic")

user = session.query(User).first()
big_orders = user.orders.filter(Order.price > 100).all()
```

4. دستی Load ( "noload" )

هیچوقت خودکار لود نمیشه.

اگه بخوای باید خودت دستی کوئری بزنی.

📌 مثال:

```python
orders = relationship("Order", lazy="noload")
user = session.query(User).first()
print(user.orders)  # خالی برمی‌گرده
```

### <span style="color:#FFB366">Advanced Querying</span>

گاهی کوئری‌های ساده کافی نیستن و باید سراغ ابزارهای پیشرفته‌تر بریم: Joins، Subquery، Union، Window Functions، Raw SQL.

#### <span style="color:#FFCC99">Complex joins</span>

📍 Inner Join (اتصال مستقیم)

فقط داده‌هایی میاره که تو هر دو جدول وجود دارن.

```python
result = session.query(User, Order)\
    .join(Order)\
    .filter(Order.total > 100)\
    .all()
# همه کاربرانی که سفارششون بیشتر از 100 باشه
```

📍 **Outer Join (اتصال بیرونی)**

حتی اگه داده در جدول دوم نباشه، رکورد جدول اول رو میاره.

```python
result = session.query(User)\
    .outerjoin(Order)\
    .filter(Order.id.is_(None))\
    .all()
# همه کاربرانی که هیچ سفارشی ندارن
```

#### <span style="color:#FFCC99">Subqueries</span>

کوئری‌ای که داخل یه کوئری دیگه استفاده میشه.

📍 **Subquery عادی**
```python
subq = session.query(Order.user_id)\
    .filter(Order.total > 1000)\
    .subquery()

rich_users = session.query(User)\
    .filter(User.id.in_(subq))\
    .all()
# کاربرانی که سفارشی بیشتر از 1000 دارن
```

📍 **Scalar Subquery**

یه مقدار تکی (مثل میانگین یا ماکس) برمی‌گردونه.

```python
avg_total = session.query(func.avg(Order.total)).scalar_subquery()

above_avg_orders = session.query(Order)\
    .filter(Order.total > avg_total)\
    .all()
# سفارش‌هایی که بیشتر از میانگین کل باشن
```

**توضیح scalar_subquery:**

```python
session.query(func.avg(Order.total)).scalar()
```
👈 این واقعاً یک عدد پایتونی برمی‌گردونه (مثلاً 125.3).
یعنی کوئری اجرا میشه الان همین لحظه و مقدار میانگین از دیتابیس میاد.
(دیگه نمی‌تونی توی کوئری‌های بعدی ازش استفاده کنی.)

```python
session.query(func.avg(Order.total)).scalar_subquery()
```
👈 این یه زیرکوئری می‌سازه که هنوز داخل دیتابیس اجرا نشده.
می‌تونی این زیرکوئری رو به‌عنوان بخشی از شرط کوئری بزرگ‌تر استفاده کنی.
scalar_subquery() خودش یک آبجکت زیرکوئری (SQL expression object) برمی‌گردونه

#### <span style="color:#FFCC99">Union operations</span>

برای ترکیب خروجی چند کوئری مختلف.

🔸 Union
نتیجه‌ی دو کوئری رو ترکیب می‌کنه بدون تکراری‌ها.

📍 **Union (بدون تکراری‌ها)**
```python
young_users = session.query(User).filter(User.age < 25)
old_users = session.query(User).filter(User.age > 65)

all_users = young_users.union(old_users).all()
# همه کاربرا، یا خیلی جوون یا خیلی پیر
```

🔸 **Union All**
نتیجه‌ی دو کوئری رو ترکیب می‌کنه با تکراری‌ها.

📍 **Union All (با تکراری‌ها)**
```python
all_users = young_users.union_all(old_users).all()
```

#### <span style="color:#FFCC99">Window functions</span>

برای تحلیل داده‌ها روی ردیف‌ها (مثل رتبه‌بندی یا شماره‌گذاری).

📍 **Row Number**
به هر ردیف یک شماره‌ی یکتا میده، صرفاً برای ترتیب.

```python
result = session.query(
    User.name,
    func.row_number().over(order_by=User.created_at).label('row_num')
).all()
# شماره ردیف برای هر کاربر بر اساس زمان ثبت‌نام
```

📍 **Rank**
رتبه میده، ولی اگه دو تا رکورد مساوی باشن رتبه‌ی یکسان می‌گیرن.

مثال ساده:
- User 1 ← سفارش 500 ← رتبه 1  
- User 1 ← سفارش 500 ← رتبه 1  
- User 1 ← سفارش 300 ← رتبه 3  

```python
result = session.query(
    Order.user_id,
    Order.total,
    func.rank().over(
        partition_by=Order.user_id,
        order_by=Order.total.desc()
    ).label('rank')
).all()
# رتبه سفارش هر کاربر بر اساس مبلغ
```

#### <span style="color:#FFCC99">Raw SQL integration</span>

وقتی کوئری خیلی پیچیده باشه یا از فانکشن خاص دیتابیس بخوای استفاده کنی.

- ()text برای نوشتن کوئری خام.
- pattern یه placeholder هست که مقدارش رو به‌صورت امن تزریق می‌کنیم.
- ()fetchall ← همه ردیف‌ها.
- ()fetchone ← فقط یک ردیف.
- fetchmany(5) ← تعداد مشخصی رکورد.
- ()from_statement وقتی می‌خوای یه کوئری خام رو به ORM وصل کنی(خروجی ORM بشه)

📍 **اجرای مستقیم SQL**
```python
result = session.execute(
    text("SELECT * FROM users WHERE name LIKE :pattern"),
    {"pattern": "احمد%"}
).fetchall()
# همه کاربرانی که اسمشون با احمد شروع بشه
```

📍 **ترکیب با ORM**
```python
users = session.query(User)\
    .from_statement(
        text("SELECT * FROM users WHERE complex_condition()")
    ).all()
```



## <span style="color:#FF8C00">Advanced Topics</span>

### <span style="color:#FFB366">Session Management Patterns</span>

در SQLAlchemy، Session مسئول مدیریت ارتباط با دیتابیس و اجرای کوئری‌هاست. روش‌های مختلفی برای مدیریت Session داریم که در فریمورک‌ها استفاده می‌شوند

#### <span style="color:#FFCC99">Session per request</span>

برای هر درخواست HTTP یک Session جدید ساخته می‌شود و بعد از پایان درخواست بسته می‌شود. این روش رایج و امن است چون Session ها بین درخواست‌ها به اشتراک گذاشته نمی‌شوند.

**مثال FastAPI**
```python
def get_db():
    db = SessionLocal()   # ایجاد یک Session جدید
    try:
        yield db          # استفاده در endpoint
    finally:
        db.close()        # بسته شدن Session بعد از پایان درخواست

@app.get("/users")
def get_users(db: Session = Depends(get_db)):
    return db.query(User).all()
```

#### <span style="color:#FFCC99">Contextual sessions</span>

گاهی چند تابع یا چند Thread باید از یک Session استفاده کنند. scoped_session این کار را انجام می‌دهد و هر Thread یک Session اختصاصی دارد.

```python
from sqlalchemy.orm import scoped_session, sessionmaker

Session = scoped_session(sessionmaker(bind=engine))

def some_function():
    user = Session.query(User).first()  # همان Session برای Thread فعلی
    return user

# پاک کردن Session بعد از اتمام کار
Session.remove()
```

- sessionmaker یک کارخانه (Factory) برای ساخت Session است.
- engine مسئول ارتباط با دیتابیس است (مانند TCP connection یا SQLite file).
- وقتی bind=engine می‌گذاری، یعنی این Session بداند که با کدام دیتابیس کار کند.

مثال:
```python
engine = create_engine("sqlite:///app.db")
Session = sessionmaker(bind=engine)
session = Session()  # این Session به "app.db" متصل است
```

#### <span style="color:#FFCC99">Thread-local sessions</span>

هر Thread خودش یک Session جداگانه دارد. مشابه scoped_session ولی دستی مدیریت می‌شود.

```python
import threading

session_registry = threading.local()

def get_session():
    if not hasattr(session_registry, 'session'):
        session_registry.session = SessionLocal()
    return session_registry.session
```

- session_registry یک فضای ذخیره‌سازی مخصوص هر Thread است (threading.local()).
- وقتی می‌نویسیم session_registry.session = SessionLocal()، داریم یک Session اختصاصی برای Thread فعلی می‌سازیم و ذخیره می‌کنیم.

#### <span style="color:#FFCC99">Session events</span>

می‌توانیم قبل یا بعد از commit/rollback تغییرات دیتابیس عملیات دلخواه انجام دهیم، مثل logging یا validation.

```python
from sqlalchemy import event

@event.listens_for(Session, 'before_commit')
def before_commit(session):
    print("قبل از Commit")

@event.listens_for(Session, 'after_commit')
def after_commit(session):
    print("بعد از Commit")
```


before_commit ← قبل از ذخیره نهایی تغییرات

after_commit ← بعد از ذخیره نهایی تغییرات

### <span style="color:#FFB366">Advanced Relationships</span>

SQLAlchemy امکانات پیشرفته‌ای برای مدل‌سازی روابط بین جدول‌ها دارد. در این بخش به مواردی مهم می‌پردازیم

#### <span style="color:#FFCC99">Self-referential relationships</span>

یک جدول می‌تواند به خودش ارجاع داشته باشد

```python
class Employee(Base):
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    manager_id = Column(Integer, ForeignKey('employees.id'))
    
    manager = relationship("Employee", remote_side=[id], back_populates="subordinates")
    subordinates = relationship("Employee", back_populates="manager")
```

remote_side در SQLAlchemy:
- وقتی یک جدول به خودش ارجاع می‌دهد (Self-referential)، SQLAlchemy باید بداند کدام ستون «سمت دیگر رابطه» است.

#### <span style="color:#FFCC99">Polymorphic relationships</span>

- می‌توان کلاس‌های فرزند را در یک ساختار مشترک ذخیره کرد و SQLAlchemy می‌فهمد هر ردیف از کدام نوع است
- وقتی داری چند نوع موجودیت داری که بعضی ستون‌هاشون مشترکه، می‌تونی از Polymorphic استفاده کنی.

```python
class Person(Base):
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    type = Column(String(20))  # مشخص می‌کنه نوعش چیه
    __mapper_args__ = {'polymorphic_on': type, 'polymorphic_identity': 'person'}

class Employee(Person):
    salary = Column(Float)
    __mapper_args__ = {'polymorphic_identity': 'employee'}

class Customer(Person):
    credit_limit = Column(Float)
    __mapper_args__ = {'polymorphic_identity': 'customer'}
```

۱. نقش __mapper_args__

این یک دیکشنری مخصوص SQLAlchemy ORM است که به کلاس می‌گوید چگونه با جدول و وراثت رفتار کند.

مخصوصاً وقتی از Polymorphic Inheritance (وراثت جدول‌ها) استفاده می‌کنیم، اینجا مشخص می‌کنیم که SQLAlchemy چطور نوع رکوردها را تشخیص دهد.

۲. polymorphic_on

polymorphic_on: type


مشخص می‌کند کدام ستون جدول نوع (Type) رکورد را نگه می‌دارد.

در مثال ما، ستون type مشخص می‌کند که این رکورد یک Person است یا Employee یا Customer.

یعنی هر رکورد وقتی در جدول ذخیره می‌شود، این ستون مقدارش تعیین می‌کند که SQLAlchemy کدام کلاس را به آن اختصاص دهد.

۳. polymorphic_identity

polymorphic_identity مقداری است که در ستون type جدول ذخیره می‌شود و مشخص می‌کند رکورد مربوط به کدام کلاس است.

این مقدار می‌تواند هر رشته‌ای باشد، ولی معمولاً خوانا و مرتبط با کلاس انتخاب می‌شود

#### <span style="color:#FFCC99">Hybrid properties</span>

می‌توان متدی در کلاس تعریف کرد که هم در Python قابل دسترسی باشد و هم در کوئری SQL استفاده شود.

```python
from sqlalchemy.ext.hybrid import hybrid_property
from sqlalchemy import func

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    first_name = Column(String(30))
    last_name = Column(String(30))
    
    @hybrid_property # for python
    def full_name(self):
        return self.first_name + ' ' + self.last_name
    
    @full_name.expression # for SQL
    def full_name(cls):
        return func.concat(cls.first_name, ' ', cls.last_name)

# استفاده
user = session.query(User).first()
print(user.full_name)  # "احمد علی"
```

وقتی بخوای از full_name در filter() یا order_by() استفاده کنی، SQLAlchemy خودش اون رو به SQL تبدیل می‌کنه:

```python
users = session.query(User).filter(User.full_name == 'احمد علی').all()
# اینجا از @full_name.expression استفاده میشه
``` 

### <span style="color:#FFB366">Customization و Extensions</span>

#### <span style="color:#FFCC99">Custom types</span>

برای زمانی که می‌خواهیم نوع داده‌ای غیر استاندارد در دیتابیس ذخیره کنیم، مثل JSON:

```python
from sqlalchemy.types import TypeDecorator, String
import json

class JSONType(TypeDecorator):
    impl = String
    
    def process_bind_param(self, value, dialect):
        return json.dumps(value) if value else value
    
    def process_result_value(self, value, dialect):
        return json.loads(value) if value else value

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    preferences = Column(JSONType())

# استفاده
user = User(preferences={'theme': 'dark', 'lang': 'fa'})
```

TypeDecorator در SQLAlchemy یعنی:

- من می‌خوام یک نوع دیتابیس سفارشی بسازم که پشت‌صحنه روی یک نوع استاندارد پیاده بشه.
- فرض کن دیتابیس فقط String و Integer و… رو می‌فهمه.
- ولی من می‌خوام یک ستون داشته باشم که بتونه دیکشنری/JSON ذخیره کنه.

impl:

- impl یعنی نوع اصلی دیتابیس که این نوع سفارشی روی اون سوار شده.
- اینجا می‌گیم: این JSONType در اصل همون String هست
- پس داخل دیتابیس یه VARCHAR/TEXT ذخیره میشه، ولی توی Python یه دیکشنری/JSON می‌بینیم.

process_bind_param:

- وقتی می‌خوای داده رو بفرستی توی دیتابیس (insert/update)، این تابع اجرا میشه.

process_result_value:

- وقتی از دیتابیس داده رو بگیری (select)، این تابع اجرا میشه.


#### <span style="color:#FFCC99">Validators</span>

با @validates می‌توان قبل از ذخیره داده، اعتبارسنجی انجام داد:

```python
from sqlalchemy.orm import validates

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    email = Column(String(100))
    age = Column(Integer)
    
    @validates('email')
    def validate_email(self, key, email):
        if '@' not in email:
            raise ValueError("ایمیل نامعتبر")
        return email
    
    @validates('age')
    def validate_age(self, key, age):
        if age < 0 or age > 150:
            raise ValueError("سن نامعتبر")
        return age
```


✅ جلوی داده‌های اشتباه قبل از Commit گرفته می‌شود.

دکوراتور @validates: 
- قبل از اینکه داده در این فیلد ذخیره بشه، اول از این تابع ردش کن
- key: اسم فیلدی که validate میشه (مثلاً 'email').
- داده اگه درست باشه، return میشه و ذخیره میشه.
- اگه اشتباه باشه، Exception میندازه.

اعتبارسنجی چند فیلد در یک تابع

اگه بخوای می‌تونی یک تابع برای چند فیلد بذاری:

```python
@validates('email', 'age')
def validate_fields(self, key, value):
    if key == 'email':
        if '@' not in value:
            raise ValueError("ایمیل نامعتبر")
    elif key == 'age':
        if value < 0 or value > 120:
            raise ValueError("سن نامعتبر")
    return value
```

#### <span style="color:#FFCC99">Events و listeners</span>

می‌توانیم به Insert، Update، Delete واکنش نشان دهیم:

```python
from sqlalchemy import event
from datetime import datetime

@event.listens_for(User, 'before_insert')
def set_created_at(mapper, connection, target):
    target.created_at = datetime.utcnow()

@event.listens_for(User, 'after_update')
def log_update(mapper, connection, target):
    print(f"User {target.id} updated")
```

#### <span style="color:#FFCC99">Mixins</span>

می‌توانیم ستون‌ها و ویژگی‌های مشترک را در یک کلاس بنویسیم و به مدل‌ها اضافه کنیم:

```python
class TimestampMixin:
    created_at = Column(DateTime, default=datetime.utcnow)
    updated_at = Column(DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)

class User(Base, TimestampMixin):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
```

#### <span style="color:#FFCC99">Custom loading techniques</span>

برای کنترل اینکه چه داده‌هایی هنگام Query بارگذاری شوند

مشکل رایج: N+1 Query Problem

وقتی لیست کاربران رو می‌گیری، و بعد برای هر کاربر جداگانه Orders یا Profile رو query می‌کنی.

این میشه ده‌ها کوئری جدا (خیلی کند).

راه‌حل: joinedload / selectinload یا Loader سفارشی.

```python
from sqlalchemy.orm import joinedload

# loader سفارشی
class UserLoader:
    @staticmethod
    def full_load():
        return [joinedload(User.orders), joinedload(User.profile)]

users = session.query(User).options(*UserLoader.full_load()).all()
```

نکته: هم میتوانم یک loder نوشتت وهم میتوان و هم میتوان دستی به این صورت نوشت

**مثال کامل FastAPI**
```python
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session, joinedload

app = FastAPI()

@app.get("/users/{user_id}/full")
def get_user_full(user_id: int, db: Session = Depends(get_db)):
    user = db.query(User)\
        .options(joinedload(User.orders), joinedload(User.profile))\
        .filter(User.id == user_id)\
        .first()
    return user
```


## <span style="color:#FF8C00">Performance و Optimization</span>

### <span style="color:#FFB366">Performance Tuning</span>

#### <span style="color:#FFCC99">Query optimization</span>

اشتباه رایج: همه داده‌ها رو بیاریم، بعد در پایتون فیلتر کنیم.

روش درست: از خود SQL برای فیلتر و محدود کردن داده‌ها استفاده کنیم.

```python
# بد: همه کاربرها، بعد در پایتون فیلتر
all_users = session.query(User).all()
active_users = [u for u in all_users if u.is_active]

# خوب: مستقیم در دیتابیس فیلتر
active_users = session.query(User).filter(User.is_active == True).all()
```


#### <span style="color:#FFCC99">Index strategies</span>

ایندکس مثل فهرست کتاب عمل می‌کنه ← به جای ورق زدن کل جدول، سریع رکورد مورد نظر پیدا میشه.

برای ستون‌هایی که زیاد سرچ/فیلتر میشن، ایندکس بزن.

🔹 **مثال:**

```python
class User(Base):
    __tablename__ = 'users'
    email = Column(String(100), index=True)  # ایندکس روی ایمیل
```

🔹 **ایندکس ترکیبی (چند ستون با هم):**

```python
Index('idx_status_date', Order.status, Order.created_at)
```

#### <span style="color:#FFCC99">Connection pooling</span>

هر بار وصل شدن به دیتابیس هزینه‌بره.

Connection Pool باعث میشه اتصال‌ها کش بشن و دوباره استفاده بشن.

🔹 **مثال:**

```python
engine = create_engine(
    "postgresql://user:pass@localhost/db",
    pool_size=20,       # 20 اتصال آماده
    max_overflow=10,    # 10 اتصال اضافی در اوج
    pool_timeout=30,    # 30 ثانیه منتظر بمونه
    pool_recycle=3600,  # هر 1 ساعت تازه‌سازی
    pool_pre_ping=True  # قبل استفاده تست کن
)
```

#### <span style="color:#FFCC99">Bulk operations</span>

به جای یکی‌یکی insert/update/delete → همه رو یکجا بزن.

🔹 **Insert:**

```python
# بد
for i in range(1000):
    session.add(User(name=f"User{i}"))
session.commit()

# خوب
users_data = [{"name": f"User{i}"} for i in range(1000)]
session.bulk_insert_mappings(User, users_data)
session.commit()
```

🔹 **Update:**

```python
# خوب
session.query(User)\
    .filter(User.last_login < old_date)\
    .update({"is_active": False})
session.commit()
```

🔹 **Delete:**

```python
session.query(LogEntry)\
    .filter(LogEntry.created_at < old_date)\
    .delete()
session.commit()
```

### <span style="color:#FFB366">Caching</span>

کش به معنی ذخیره موقت داده‌ها در حافظه است تا دفعه بعدی که به همان داده‌ها نیاز داریم، دیگر به دیتابیس مراجعه نکنیم و پاسخ سریع‌تر باشد.

**انواع کش و کاربردها**

۱. کش ساده درون‌پردازشی (in-process cache)

- محل ذخیره: حافظهٔ همان پروسس Python.

- محدودیت: فقط برای همان پروسس است و در چند سرور یا چند پروسس به اشتراک گذاشته نمی‌شود.

- مثال مفهومی: یک دیکشنری ساده که نتایج کوئری را نگه می‌دارد.

- استفاده رایج: functools.lru_cache برای ذخیره نتایج تابع.

۲. کش پراسس مشترک (distributed cache)

- محل ذخیره: سیستم بیرونی مثل Redis یا Memcached.

- همهٔ پروسس‌ها و سرورها می‌توانند از آن استفاده کنند.

- می‌توان TTL (زمان انقضا) برای داده‌ها تعریف کرد.

- نیازمند سریال‌سازی داده‌ها است (JSON یا pickle).

۳. Second-level cache (SQLAlchemy)

- SQLAlchemy خودش کشی در سطح مدل و session دارد.

- مفهوم: یک رکورد از دیتابیس که بار اول خوانده شده، در cache سطح دوم نگه داشته می‌شود تا Session بعدی بتواند بدون مراجعه به دیتابیس آن را استفاده کند.

- مثال مفهومی: کاربر با id=1 بار اول از دیتابیس خوانده شد، بار دوم از کش داخلی SQLAlchemy برمی‌گردد.

۴. Dogpile.cache (Cache حرفه‌ای)

- یک ابزار قدرتمند برای مدیریت کش.

- منطقه‌های کش (Region) قابل تنظیم.

- TTL (زمان انقضا) و invalidation خودکار.

- پشتیبانی از Redis، Memcached، و حافظهٔ داخلی.

- مفهوم: توابع یا کوئری‌ها را wrap می‌کند و نتایج را به‌صورت امن در کش می‌گذارد.

- پاک‌سازی کش (invalidation) بعد از تغییر داده‌ها ضروری است تا stale data برنگردد.

#### <span style="color:#FFCC99">Query result caching</span>

**کش ساده با functools.lru_cache**

ایده: نتایج یک تابع را در حافظه نگه می‌داریم تا دفعه بعدی بدون رفتن به دیتابیس، همان نتیجه را برگرداند.

```python
from functools import lru_cache

# تابعی که کاربر را از دیتابیس می‌خواند
@lru_cache(maxsize=100)  # حداکثر 100 نتیجه در حافظه نگه داشته شود
def get_user_by_email(email):
    print("Querying DB for", email)
    return session.query(User).filter(User.email == email).first()

# استفاده
user1 = get_user_by_email("test@example.com")  # این بار از دیتابیس خوانده می‌شود
user2 = get_user_by_email("test@example.com")  # این بار از کش خوانده می‌شود
```

#### <span style="color:#FFCC99">Second-level cache</span>

هدف: داده‌هایی که بین چند Session یا Thread مشترک هستند، در یک کش مرکزی نگه داشته شود.

برخلاف کش ساده‌ی Session (که فقط در همان Session فعال است)، این کش بین Sessionهای مختلف قابل استفاده است.

```python
from sqlalchemy_utils import CacheManager

# راه‌اندازی Cache Manager
cache_manager = CacheManager()

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
    
    # Cache برای این مدل
    cache = cache_manager.cache

# استفاده
user = session.query(User).filter(User.id == 1).first()  # از DB
user = session.query(User).filter(User.id == 1).first()  # از Cache
```

#### <span style="color:#FFCC99">Dogpile.cache integration</span>

یک کتابخانه مخصوص کش که امکانات پیشرفته دارد، مثل invalidation خودکار و TTL.

**نصب و راه‌اندازی:**
```bash
pip install dogpile.cache
```

```python
from dogpile.cache import make_region

# تنظیم Region
region = make_region().configure(
    'dogpile.cache.memory',  # حافظه داخلی؛ می‌توان Redis هم استفاده کرد
    expiration_time=600      # 10 دقیقه
)

@region.cache_on_arguments()
def get_user_profile(user_id):
    return session.query(User).filter(User.id == user_id).first()

# استفاده
user = get_user_profile(1)  # بار اول از DB
user = get_user_profile(1)  # بار دوم از کش

# پاک کردن کش بعد از تغییر دیتا
def update_user(user_id, **kwargs):
    session.query(User).filter(User.id == user_id).update(kwargs)
    session.commit()
    
    region.delete(f"get_user_profile|{user_id}")  # پاک کردن کش
```
✅ نکته:

cache_on_arguments() به طور خودکار کلید کش می‌سازد.

بعد از آپدیت دیتا، حتما کش را پاک کنیم تا داده تازه برگردد.

## <span style="color:#FF8C00">Advanced Features</span>

### <span style="color:#FFB366">Migrations با Alembic</span>

وقتی مدل‌هات (models.py) تغییر می‌کنن (مثلاً یه ستون یا جدول اضافه می‌کنی)، دیتابیس به‌صورت خودکار تغییر نمی‌کنه.

Migration ابزاریه که تغییرات رو قدم به قدم ثبت و روی دیتابیس اعمال می‌کنه، مثل نسخه‌بندی برای دیتابیس.

#### <span style="color:#FFCC99">Migration basics</span>

**نصب و راه‌اندازی:**
```bash
pip install alembic

# شروع پروژه
alembic init alembic
```

یک پوشه‌ی alembic/ ساخته میشه.

داخلش env.py هست که باید Base.metadata رو بهش بدی (تا بفهمه مدل‌ها چیه).

داخل alembic.ini آدرس دیتابیس رو می‌ذاری:

```ini
# تنظیم alembic.ini
sqlalchemy.url = postgresql://user:pass@localhost/dbname
```

#### <span style="color:#FFCC99">Auto-generating migrations</span>

وقتی مدل تغییر کرد (مثلاً User اضافه شد):

```bash
alembic revision --autogenerate -m "Add user table"
alembic upgrade head
```


دستور اول یک فایل migration در alembic/versions/ می‌سازه.

دستور دوم اون migration رو روی دیتابیس اجرا می‌کنه.

برای برگشت:

```bash
alembic downgrade -1   # یک migration برگرد عقب
```

یعنی upgrade اعمال می‌کنه، downgrade برعکسش رو.

**مثال ساده Migration تولیدشده**
```python
def upgrade():
    op.create_table(
        'users',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('name', sa.String(50)),
        sa.Column('email', sa.String(100))
    )

def downgrade():
    op.drop_table('users')
```

#### <span style="color:#FFCC99">Manual migrations</span>

Manual Migration یعنی وقتی خودکار (autogenerate) کافی نیست — باید دستی Schema و/یا داده‌ها را تغییر دهی.

Manual Migration یعنی شما یک revision خالی می‌سازید (alembic revision -m "...") و داخل upgrade() و downgrade() خودتان کدهای op.* و SQL لازم را می‌نویسید.

🔸 **قالب کلی یک فایل migration**
```python
# versions/xxxx_custom_migration.py
from alembic import op
import sqlalchemy as sa

revision = 'xxxx'
down_revision = 'prev_rev'
branch_labels = None
depends_on = None

def upgrade():
    # دستوراتی که هنگام بالا بردن باید اجرا شود
    pass

def downgrade():
    # معکوس upgrade برای بازگشت
    pass
```


نکته: همیشه یک downgrade() بنویس حتی اگر ساده باشد تا در صورت نیاز بتوانی برگردی.

**این یخش کمی تخضضی تر است و از گفتن در اینجا اجتناب میشود**

#### <span style="color:#FFCC99">Branching و merging</span>

وقتی چند نفر روی پروژه کار می‌کنن، هرکسی ممکنه migration خودش رو بسازه → migrationها شاخه‌ای میشن.

**ساخت branch:**

```bash
alembic revision -m "Feature A" --branch-label=feature_a
```

**ادغام چند migration:**

```bash
alembic merge -m "merge features" head1 head2
```

**دیدن تاریخچه:**

```bash
alembic history --verbose
```

**دیدن وضعیت فعلی دیتابیس:**

```bash
alembic current
```

**Migration مثل git commit برای دیتابیسه.**

### <span style="color:#FFB366">Testing</span>

#### <span style="color:#FFCC99">Testing patterns</span>

@pytest.fixture چیست؟

در pytest، Fixture یک راهکار برای آماده‌سازی داده‌ها، منابع، یا محیط تست است.

به جای اینکه در هر تست دوباره چیزهایی مثل Session یا داده بسازیم، Fixture این کار را یک بار انجام می‌دهد و به تست‌ها تزریق می‌شود.

scope="session" یعنی چه؟

Fixture می‌تواند طول عمر مختلف داشته باشد:

- function (پیش‌فرض): هر تست یک نمونه جدید دریافت می‌کند.

- class: هر کلاس تست یک نمونه دارد.

- module: هر ماژول یک نمونه.

- session: کل تست‌ها در یک اجرا یک نمونه مشترک دارند.

**Setup تست**

از SQLite in-memory برای تست سریع استفاده می‌کنیم:

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from myapp.models import Base
import pytest

@pytest.fixture(scope="session")
def test_engine():
    engine = create_engine("sqlite:///:memory:")  # پایگاه داده موقت در حافظه
    Base.metadata.create_all(engine)
    return engine

@pytest.fixture
def session(test_engine):
    Session = sessionmaker(bind=test_engine)
    session = Session()
    yield session
    session.rollback()   # بعد از هر تست همه تغییرات برگردانده شود
    session.close()
```


هر تست یک Session تازه دارد، پس تغییرات بین تست‌ها تداخل ندارد.

scope session یعنی ایجاد engine فقط یک بار برای کل تست‌ها.

**تست ساده مدل‌ها**
```python
def test_create_user(session):
    user = User(name="احمد", email="ahmad@test.com")
    session.add(user)
    session.commit()
    
    assert user.id is not None   # کاربر ساخته شد
    assert user.name == "احمد"
```

**تست رابطه‌ها**
```python
def test_user_relationships(session):
    user = User(name="علی")
    order = Order(total=100.0)
    user.orders.append(order)
    
    session.add(user)
    session.commit()
    
    assert len(user.orders) == 1
    assert user.orders[0].total == 100.0
```

#### <span style="color:#FFCC99">Fixtures</span>

می‌توانیم نمونه‌های آماده بسازیم و در چندین تست استفاده کنیم:

```python
@pytest.fixture
def sample_user(session):
    user = User(name="کاربر تست", email="test@example.com")
    session.add(user)
    session.commit()
    return user
```

#### <span style="color:#FFCC99">Mock strategies</span>

فرض کنید تابعی به API خارجی یا سرویس دیگر متصل می‌شود، ما نمی‌خواهیم هر بار تست این سرویس واقعی را صدا بزند.

Mock یعنی جایگزین کردن واقعی با نسخه‌ی شبیه‌سازی شده که نتیجه دلخواه برگرداند.

#### <span style="color:#FFCC99">Database testing</span>

تست‌های پایگاه داده واقعی

می‌توانیم PostgreSQL واقعی یا MySQL استفاده کنیم:

```python
@pytest.fixture(scope="session")
def postgres_engine():
    engine = create_engine("postgresql://test_user:test_pass@localhost/test_db")
    Base.metadata.create_all(engine)
    yield engine
    Base.metadata.drop_all(engine)

@pytest.fixture
def postgres_session(postgres_engine):
    Session = sessionmaker(bind=postgres_engine)
    session = Session()
    yield session
    session.rollback()
    session.close()
```

مزیت: تست روی پایگاه داده واقعی انجام می‌شود، اشکالات واقعی SQL پیدا می‌شوند.

## <span style="color:#FF8C00">Real-world Applications</span>

### <span style="color:#FFB366">Design Patterns</span>

#### <span style="color:#FFCC99">Repository pattern</span>

چیست؟
یک لایه بین کدهای اپلیکیشن و دیتابیس ایجاد می‌کند تا دسترسی به داده‌ها مرتب و استاندارد شود. یعنی به جای اینکه مستقیم session.query(User) بنویسید، از یک Repository استفاده می‌کنید.

مزیت:

جداسازی منطق دیتابیس از بیزینس لایه

راحت‌تر کردن تست‌ها

تغییر دیتابیس بدون تغییر کل کد

**مثال ساده:**

```python
# repository.py
class UserRepository:
    def __init__(self, session):
        self.session = session

    def get_by_id(self, user_id):
        return self.session.query(User).filter(User.id == user_id).first()

    def add(self, user):
        self.session.add(user)
        self.session.commit()

# استفاده
repo = UserRepository(session)
user = repo.get_by_id(1)
repo.add(User(name="Ali"))
```


✅ نتیجه: کل اپلیکیشن به Repository وابسته است، نه مستقیم به Session یا SQLAlchemy.

#### <span style="color:#FFCC99">Unit of Work</span>

چیست؟
یک الگو برای مدیریت تراکنش‌ها و Session‌ها. اطمینان می‌دهد که همه تغییرات به صورت یکجا commit یا rollback شوند.

**مثال ساده:**

```python
class UnitOfWork:
    def __init__(self, session_factory):
        self.session_factory = session_factory

    def __enter__(self):
        self.session = self.session_factory()
        return self.session

    def __exit__(self, exc_type, exc_val, exc_tb):
        if exc_type:
            self.session.rollback()
        else:
            self.session.commit()
        self.session.close()

# استفاده
with UnitOfWork(Session) as session:
    user = User(name="Ahmad")
    session.add(user)  # اگر خطایی باشد rollback می‌شود
```

نکته مهم:
متدهای __enter__ و __exit__ خودکار اجرا می‌شوند وقتی که از with استفاده می‌کنید.

وقتی with UnitOfWork(Session) as session: می‌نویسید، Python خودش __enter__ را صدا می‌زند و نتیجه (session) را به شما می‌دهد.

- وقتی بلاک with تمام می‌شود (حتی اگر خطا رخ داده باشد)، Python خودش __exit__ را صدا می‌زند.

- داخل __exit__ ما مشخص کرده‌ایم:

- اگر خطا بود rollback()

- اگر خطا نبود commit()

- بعد هم Session بسته می‌شود با close()

#### <span style="color:#FFCC99">Data Mapper</span>

چیست؟
SQLAlchemy خودش از این الگو استفاده می‌کند. ایده اصلی: کلاس‌های Python به جدول‌های دیتابیس Map شوند و کلاس‌ها به صورت مستقل از دیتابیس عمل کنند.

- کلاس‌ها فقط داده نگه می‌دارند و منطق بیزینسی.

- Session / Mapper مسئول ذخیره‌سازی و بارگذاری داده‌هاست.

**مثال ساده:**

```python
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

# Mapper جدا از کلاس User
user = User(name="Sara")
session.add(user)
session.commit()
```


Mapper همین Base و SQLAlchemy ORM است که پشت صحنه کلاس User را به جدول users نگاشت می‌کند.

شما اصلاً SQL ننوشته‌اید.

Mapper این کار را انجام می‌دهد: تبدیل User به یک INSERT INTO users ... و ارسال به دیتابیس.

✅ یعنی Mapper همان چیزی است که بین کلاس پایتون و جدول دیتابیس ارتباط برقرار می‌کند.

✅ نتیجه: کلاس‌های شما مستقل هستند و دیتابیس فقط با Mapper و Session کار می‌کند.

#### <span style="color:#FFCC99">Active Record considerations</span>

چیست؟
یک الگو که در آن کلاس هم داده و هم منطق دیتابیس را در خود دارد. مثلاً کلاس خودش Save، Update و Delete را انجام می‌دهد.

این الگو در Django ORM یا Rails زیاد دیده می‌شود.

SQLAlchemy می‌تواند شبیه Active Record شود اما Data Mapper بیشتر توصیه می‌شود چون انعطاف بیشتری دارد.

**مثال ساده Active Record-style:**

```python
class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))

    def save(self, session):
        session.add(self)
        session.commit()

# استفاده
user = User(name="Neda")
user.save(session)  # کلاس خودش داده را ذخیره کرد
```

### **جمع بندی:**

1️⃣ Session

کار اصلی: مدیریت همه تعاملات با دیتابیس.

وظایفش:

- گرفتن داده‌ها (query)

- اضافه کردن یا حذف کردن رکوردها (add, delete)

- commit و rollback تراکنش‌ها

- نگه داشتن وضعیت Objectها (Transient, Pending, Persistent, Detached)

می‌توانی فکر کنی: Session مثل یک دفتر کار است که تمام تغییرات روی دیتابیس را ثبت و مدیریت می‌کند.

2️⃣ Mapper (یا ORM)

کار اصلی: نگاشت کلاس‌های Python به جدول‌های دیتابیس.

وظایفش:

- مشخص کردن چه کلاس Python‌ای مربوط به کدام جدول است (Declarative Base)

- تبدیل Objectها به SQL و برعکس

- مدیریت روابط بین کلاس‌ها (One-to-Many, Many-to-Many, Polymorphic)

می‌توانی فکر کنی: Mapper همان پلی بین کلاس‌های Python و جدول‌های دیتابیس است.

### <span style="color:#FFB366">Integration</span>

#### <span style="color:#FFCC99">Web framework integration (Flask, FastAPI)</span>

اینجا هدف این است که SQLAlchemy را در کنار یک فریمورک وب استفاده کنیم تا Requestها بتوانند به راحتی با دیتابیس کار کنند.

**FastAPI مثال:**

```python
from fastapi import FastAPI, Depends
from sqlalchemy.orm import Session
from database import SessionLocal, User

app = FastAPI()

# Session per Request
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get("/users/{user_id}")
def get_user(user_id: int, db: Session = Depends(get_db)):
    return db.query(User).filter(User.id == user_id).first()
```

#### <span style="color:#FFCC99">Async SQLAlchemy</span>

نسخه async برای کار با دیتابیس به صورت غیرهمزمان در فریمورک‌هایی مثل FastAPI یا Starlette استفاده می‌شود.

```python
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession
from sqlalchemy.orm import sessionmaker
from models import User

engine = create_async_engine("postgresql+asyncpg://user:pass@localhost/db")
AsyncSessionLocal = sessionmaker(engine, class_=AsyncSession, expire_on_commit=False)

async def get_user(user_id: int):
    async with AsyncSessionLocal() as session:
        result = await session.get(User, user_id)
        return result
```
✅ نکته: Async برای اپلیکیشن‌هایی با I/O بالا بسیار مناسب است و جلوی بلاک شدن event loop را می‌گیرد.

#### <span style="color:#FFCC99">Multi-database setups</span>

گاهی پروژه چند دیتابیس دارد (مثلاً خواندن و نوشتن جدا یا دیتابیس‌های مختلف برای ماژول‌ها). SQLAlchemy اجازه تعریف چند engine و Session می‌دهد.

```python
# دو Engine برای دو دیتابیس مختلف
engine_main = create_engine("postgresql://user:pass@main_db")
engine_logs = create_engine("postgresql://user:pass@logs_db")

SessionMain = sessionmaker(bind=engine_main)
SessionLogs = sessionmaker(bind=engine_logs)

# استفاده
with SessionMain() as main_session, SessionLogs() as log_session:
    user = main_session.query(User).first()
    log_session.add(LogEntry(message="Fetched user"))
    log_session.commit()
```

#### <span style="color:#FFCC99">Sharding strategies</span>

Sharding یعنی تقسیم داده‌ها روی چند دیتابیس برای مقیاس‌پذیری. SQLAlchemy خودش Sharding را مدیریت می‌کند.

```python
from sqlalchemy.ext.horizontal_shard import ShardedSession

# فرض کنید دو دیتابیس داریم
shards = {
    'shard_1': create_engine('postgresql://user:pass@db1'),
    'shard_2': create_engine('postgresql://user:pass@db2')
}

def shard_chooser(mapper, instance, clause=None):
    # تصمیم گیری برای اینکه رکورد کجا برود
    return 'shard_1' if instance.id % 2 == 0 else 'shard_2'

session = ShardedSession(shards=shards, shard_chooser=shard_chooser)

user = User(id=5, name="Ali")
session.add(user)  # خودکار روی shard مناسب می‌رود
session.commit()
```


✅ نکته: Sharding بیشتر برای دیتابیس‌های بزرگ و مقیاس‌پذیر استفاده می‌شود.

---

## <span style="color:#FF6B35">🎉 پایان مرجع جامع SQLAlchemy</span>

### <span style="color:#FFB366">تبریک! 🎊</span>

شما با موفقیت یکی از **کامل‌ترین و جامع‌ترین مراجع فارسی SQLAlchemy** را مطالعه کردید. این مرجع شامل:

- ✅ **مفاهیم پایه** از صفر تا صد
- ✅ **تکنیک‌های پیشرفته** برای پروژه‌های واقعی  
- ✅ **بهترین روش‌ها** (Best Practices) در صنعت
- ✅ **الگوهای طراحی** حرفه‌ای
- ✅ **بهینه‌سازی عملکرد** و کش
- ✅ **تست و Migration** با Alembic
- ✅ **ادغام با فریمورک‌های وب** مدرن

### <span style="color:#FFB366">پیشنهادات بعدی 🚀</span>

حالا که SQLAlchemy را به خوبی یاد گرفته‌اید:

1. **پروژه عملی بسازید** - بهترین راه یادگیری، تمرین است
2. **با FastAPI ترکیب کنید** - برای ساخت API های مدرن
3. **Async SQLAlchemy امتحان کنید** - برای اپلیکیشن‌های پرترافیک
4. **PostgreSQL پیشرفته یاد بگیرید** - برای استفاده بهینه از قابلیت‌ها

### <span style="color:#FFB366">تشکر ویژه 🙏</span>

از **صبر و همراهی شما** در این سفر یادگیری تشکر می‌کنیم. امیدواریم این مرجع برای شما مفید بوده و در پروژه‌های آینده‌تان کمک‌تان کند.

### <span style="color:#FFB366">در تماس باشیم 📫</span>

اگر سوال، پیشنهاد، یا نیاز به راهنمایی بیشتر داشتید، خوشحال می‌شویم کمک‌تان کنیم.

**موفق و پیروز باشید! 💪**

---

<div align="center">

**🌟 ساخته شده با ❤️ برای جامعه توسعه‌دهندگان فارسی‌زبان 🌟**

</div>