### 1 array的增删改

- 1.增加和删除注意点，用pull 和push, 

  - 增加, 注意多个时用each

    ```go
    bson.M{operator.Push: bson.M{property:bson.M{operator.Each:arrs}}}
    ```

  - 删除，注意多个时用in

    ```go
    bson.M{operator.Pull: bson.M{property:bson.M{operator.In:arrs}}}
    ```

    

