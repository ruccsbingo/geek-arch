@startuml
autonumber
participant 应用服务器  as app 
participant "存储服务（序列1服务器NO.2）（故障）" as store1
participant "存储服务（序列2服务器NO.2）" as store2
participant 临时服务器 as tmp
app -> store2 : 读数据（只从正常服务器读）
app -> store2 : 写数据
app -> tmp : 故障服务器恢复服务前，写入数据
store1 <- tmp : 故障服务器恢复后，从临时挂起迁移故障期间写入的数据
app -> store1 : 迁移完成，恢复正常写入 
app -> store2 : 迁移完成，恢复正常写入 
@enduml


![](http://www.plantuml.com/plantuml/png/ZP9FIiD05CRtESNGVOLcAI8zWPuXQXO5auPaSe0MAwaaRHSjiQKW_X6BqEgYQcW2NgPlagvo1TymOs0GfBjavllztljWcXurNEfRbvhXqxRjMsUcgpbur3flEOPD2Mp6-NZ1vX7StCDqGOZX4SDnY1AgmV8MkZ9LPW5iXX34ZOewEJtGowoFDspIsytc-5tZ8e-sNREnXqfNL0gkA_WsMRFuiqhp5BKSZMzSFvO0EIJ5MyecxonQyGd3rsqwOCj7I98An01E-SF1zLHmyeRByLYqgc3MUO2dIFxsep8BaOFUiqH5Qt9K_u-6qG0vN4ms2hl5nrVntSbVqj_ytIvU2t4-krBN4YFGBGXOXImOeK-uHLU14hNZVaZJj2_ucz6q7m00)