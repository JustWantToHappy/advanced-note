## 一对一关系
```
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
