## Outline
Bug reproduction repo of Prisma, when `@db.timestampz` typed column being used.

Prisma schema file is here: [src/schema.prisma](https://github.com/samchon/prisma-bug-report-postgres-timestampz/blob/master/src/schema.prisma)

You can reproduce the bug like below:

```bash
git clone https://github.com/samchon/prisma-bug-report-postgres-timestampz
cd prisma-bug-report-postgres-timestampz

npm install
npm run build:schema
```




## Story
Such bug does not appear when testing other schema models.

For reference, `src/schema.prisma` file has lots of comments (`///`). It's just my style that describing each tables and columns into the prisma schema file. Also, there're some comment tags like `@format uuid`. It's just for validation of input data before data archiving through [typia](https://github.com/samchon/typia), not for `prisma`. Therefore, don't mind about those comments please.

By the way, I tried to erase those all comments, but same bug still occurs.




## Error Message
```bash
> prisma-bug-report-postgres-timestampz@1.0.0 build:prisma
> prisma generate --schema=src/schema.prisma

Prisma schema loaded from src\schema.prisma
Error: Prisma schema validation - (get-dmmf wasm)
Error code: P1012
error: Native type Timestampz is not supported for postgresql connector.
  -->  schema.prisma:66
   | 
65 |   /// 레코드 생성 일시.
66 |   created_at DateTime @db.Timestampz
   | 
error: Native type Timestampz is not supported for postgresql connector.
  -->  schema.prisma:146
   | 
145 |   /// 레코드 생성 일시
146 |   created_at DateTime @db.Timestampz
   | 
error: Native type Timestampz is not supported for postgresql connector.
  -->  schema.prisma:206
   | 
205 |   /// 결제 취소 시간.
206 |   created_at DateTime @db.Timestampz
   | 
error: Native type Timestampz is not supported for postgresql connector.
  -->  schema.prisma:257
   | 
256 |   /// 웹훅 레코드 생성 일시.
257 |   created_at DateTime @db.Timestampz
   | 
error: Native type Timestampz is not supported for postgresql connector.
  -->  schema.prisma:308
   | 
307 |   /// 레코드 생성 일시.
308 |   created_at DateTime @db.Timestampz
   | 

Validation Error Count: 5
[Context: getDmmf]

Prisma CLI Version : 4.16.2
```