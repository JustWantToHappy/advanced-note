## prisma的几个常用命令
1. npx prisma migrate deploy：用于将新的迁移应用于数据库。在运行此命令之前，您需要先创建迁移文件。
2. npx prisma migrate reset：用于将数据库重置为初始状态。当您想要修改或回滚迁移并需要重新应用迁移时，可以使用此命令。请注意，此命令将清除所有数据库中的表格，而不仅仅是清除迁移内容，务必谨慎操作。
3. npx prisma migrate dev --name init：该命令结合了 prisma migrate deploy 和 prisma generate 两个命令，它将会为您的数据库执行一个全新的初始化操作，并且自动迁移最新的数据模式，同时生成新的客户端代码
4. npx prisma generate --watch 实时监听schema，如果schema发生变化就会执行，并生成最新的prisma客服端代码。
5. npx prisma generate重新生成prisma客服端代码
6. npx prisma studio:prisma图像化界面

mongodb,如果需要将schema应用到数据库，需要运行:npx prisma db push(prisma占不支持mongodb的数据迁移)
## 一对一关系
```graphql
model User{
    id       String    @id @default(uuid())
    profile  Profile?
}

model Profile{
    id       Int       @id @default(autoincrement())
    userId   String    @unique
    student  Student   @relation(fields: [userId], references: [id])
}
```
## 创建多对多关系
```graphql
model User{
    id        String     @id @default(uuid())
    UserRole  UserRole[]
}
model Role {
  id        Int        @id @default(autoincrement())
  UserRole  UserRole[]
}
model UserRole {
  id     Int    @id @default(autoincrement())
  roleId Int
  role   Role   @relation(fields: [roleId], references: [id])
  userId String
  user   User   @relation(fields: [userId], references: [id])
  //自定义表名
  @@map("user_role")
}
```