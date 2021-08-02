# FireBase实时数据库接入
## 环境配置
-  在项目的gradle文件引入
```
    dependencies {
      classpath 'com.google.gms:google-services:4.3.8'  // Google Services plugin
    }
```

- 在app的gradle文件引入：
```
plugins {
    id 'com.google.gms.google-services'
}

android {
    defaultConfig {
    // 这里的包名要和服务器配置一致
        applicationId "com.test"
       }
}

dependencies {
    implementation 'com.google.firebase:firebase-database:19.2.1'
    implementation platform('com.google.firebase:firebase-bom:28.2.1')
}
```

- 将下载的google-services.json文件放在app目录下

## 开始使用
```kotlin
 fun writeAndRead(){
        // Write a message to the database
        // Write a message to the database
        val database = FirebaseDatabase.getInstance()
        val myRef = database.getReference("key")

        myRef.setValue("Hello, World!11")

        // Read from the database
        myRef.addValueEventListener(object : ValueEventListener {
            override fun onDataChange(dataSnapshot: DataSnapshot) {
                // This method is called once with the initial value and again
                // whenever data at this location is updated.
                val value = dataSnapshot.getValue(String::class.java)
                Log.d("TAG", "Value is: $value")
            }

            override fun onCancelled(error: DatabaseError) {
                // Failed to read value
                Log.w("TAG", "Failed to read value.", error.toException())
            }
        })
```

## [Demo地址](https://github.com/loyal888/FireBaseDemo)