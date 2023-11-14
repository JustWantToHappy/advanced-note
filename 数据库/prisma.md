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