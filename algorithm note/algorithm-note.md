### title

### 创建索引

1. **单字段索引**：
   - `db.collection.createIndex({ field: 1 })`：创建升序索引。
   - `db.collection.createIndex({ field: -1 })`：创建降序索引。
   - 示例：
     ```bash
     db.users.createIndex({ firstName: 1 })
     ```


2. **复合索引**：
   - `db.collection.createIndex({ field1: 1, field2: -1 })`：创建多字段索引。
   - 示例：
     ```bash
     db.users.createIndex({ firstName: 1, lastName: -1 })
     ```

3. **唯一索引**：
   - `db.collection.createIndex({ field: 1 }, { unique: true })`：创建唯一索引，确保字段值的唯一性。
   - 示例：
     ```bash
     db.users.createIndex({ email: 1 }, { unique: true })
     ```

4. **稀疏索引**：
   - `db.collection.createIndex({ field: 1 }, { sparse: true })`：创建稀疏索引，仅索引包含该字段的文档。
   - 示例：
     ```bash
     db.users.createIndex({ middleName: 1 }, { sparse: true })
     ```

   稀疏索引（Sparse Index）是一种特殊类型的索引，它只包含那些包含被索引字段的文档。对于不包含该字段的文档，MongoDB 会忽略它们，不会将其添加到索引中。

5. **TTL（Time-To-Live）索引**：
   - `db.collection.createIndex({ field: 1 }, { expireAfterSeconds: <seconds> })`：创建 TTL 索引，自动删除过期文档。
   - 示例：
     ```bash
     db.logs.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 })
     ```
   该命令会为 `createdAt` 字段创建一个 TTL 索引，文档将在创建后 3600 秒（即 1 小时）自动删除。

---

### 查看索引

1. **显示集合的所有索引**：
   - `db.collection.getIndexes()`：显示集合上的所有索引。
   - 示例：
     ```bash
     db.users.getIndexes()
     ```

2. **显示集合的索引信息**：
   - `db.collection.indexInformation()`：显示集合的索引信息，包括每个索引的字段和排序顺序。
   - 示例：
     ```bash
     db.users.indexInformation()
     ```

---

### 删除索引

1. **删除单个索引**：
   - `db.collection.dropIndex("<index_name>")`：删除指定的索引。
   - 示例：
     ```bash
     db.users.dropIndex("firstName_1")
     ```

2. **删除所有索引**：
   - `db.collection.dropIndexes()`：删除集合上的所有索引。
   - 示例：
     ```bash
     db.users.dropIndexes()
     ```

---

### 其他索引管理命令

1. **重建索引**：
   - `db.collection.reIndex()`：重建集合上的所有索引。如果有索引损坏或者需要优化索引，可以使用该命令。
   - 示例：
     ```bash
     db.users.reIndex()
     ```

2. **查看索引使用情况**：
   - `db.collection.explain("executionStats").find(<query>).hint(<index>)`：使用 `explain` 方法查看查询的执行计划，确认索引是否有效。
   - 示例：
     ```bash
     db.users.explain("executionStats").find({ firstName: "John" }).hint({ firstName: 1 })
     ```

3. **查看索引大小**：
   - `db.collection.totalIndexSize()`：显示集合上所有索引的总大小。
   - 示例：
     ```bash
     db.users.totalIndexSize()
     ```

4. **查看单个索引大小**：
   - `db.collection.indexSizes()`：显示集合上每个索引的大小。
   - 示例：
     ```bash
     db.users.indexSizes()
     ```

---

通过这些索引命令，可以有效地管理 MongoDB 中的索引结构，优化查询性能，并确保数据访问的高效性。在使用 MongoDB 时，合理设计和管理索引对于数据库性能至关重要。