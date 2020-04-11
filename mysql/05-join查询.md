# SQL执行顺序

![1582273349204](assets/1582273349204.png)

# 7种join连接

## 内连接

### 内连接文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-27e9668b8ec1b888.png?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

执行的sql语句以及执行的查询结果

- 执行的sql语句

```mysql
select * from tbl_dept a inner join tbl_emp b on a.id=b.deptId;
```

- 查询结果

  ![img](https:////upload-images.jianshu.io/upload_images/11273713-5228b626093d2f2e.png?imageMogr2/auto-orient/strip|imageView2/2/w/708/format/webp)


## 左外连接

### 左外连接文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-e473166073a067a8.png?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```csharp
select * from tbl_dept a left join tbl_emp b on a.id=b.deptId;
```

- 查询结果

  ![img](https:////upload-images.jianshu.io/upload_images/11273713-dee834ef1ee0a54e.png?imageMogr2/auto-orient/strip|imageView2/2/w/710/format/webp)


## 右外连接

### 右外连接文氏图



![img](https:////upload-images.jianshu.io/upload_images/11273713-6bd43314a7545fc4.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

这里写图片描述

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```csharp
select * from tbl_dept a right join tbl_emp b on a.id=b.deptId;
```

- 查询结果

  ![img](https:////upload-images.jianshu.io/upload_images/11273713-b57412902dcb896e.png?imageMogr2/auto-orient/strip|imageView2/2/w/632/format/webp)


## 左连接

### 左连接文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-951301e32958eb0c.png?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```csharp
elect * from tbl_dept a left join tbl_emp b on a.id=b.deptId where b.deptId is null;
```

- 查询结果

![img](https:////upload-images.jianshu.io/upload_images/11273713-5e3542c44821fdb7.png?imageMogr2/auto-orient/strip|imageView2/2/w/710/format/webp)

## 右连接

### 右连接文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-1786d2c30e13e81e.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

右连接

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```csharp
select * from tbl_dept a right join tbl_emp b on a.id=b.deptId where a.id is null;
```

- 查询结果

![img](https:////upload-images.jianshu.io/upload_images/11273713-5a89ba4840496d0d.png?imageMogr2/auto-orient/strip|imageView2/2/w/630/format/webp)

右连接

## 全连接

### 全连接文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-284185d77bef02f4.png?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

这里写图片描述

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```mysql
select * from tbl_dept a right join tbl_emp b on a.id=b.deptId 
union 
select * from tbl_dept a left join tbl_emp b on a.id=b.deptId;
```

- 查询结果

  ![img](https:////upload-images.jianshu.io/upload_images/11273713-87f51718d1d49125.png?imageMogr2/auto-orient/strip|imageView2/2/w/645/format/webp)

  全连接

## 两张表中都没有出现的数据集

### 文氏图

![img](https:////upload-images.jianshu.io/upload_images/11273713-7e1a43054dacacfc.png?imageMogr2/auto-orient/strip|imageView2/2/w/300/format/webp)

#### 执行的sql语句以及执行的查询结果

- 执行的sql语句

```csharp
select * from tbl_dept a right join tbl_emp b on a.id=b.deptId where a.id is null 
union 
select * from tbl_dept a left join tbl_emp b on a.id=b.deptId where b.deptId is null;
```

- 查询结果

![img](https:////upload-images.jianshu.io/upload_images/11273713-9fe1283c1679ab84?imageMogr2/auto-orient/strip|imageView2/2/w/647/format/webp)