# DESCrypt
DES加密解密
### 中文会出现乱码，需要用Base64解码
### 代码如下
```
object DESCrypt{
    //des加密
    fun encrypt(input:String,password:String): String {
        //1.创建cipher对象
        val cipher = Cipher.getInstance("DES")

        //2.初始化cipher(参数：加密/解密模式)
        val kf = SecretKeyFactory.getInstance("DES")
        val keySpec = DESKeySpec(password.toByteArray())

        val key: Key = kf.generateSecret(keySpec)
        cipher.init(Cipher.ENCRYPT_MODE,key)

        //加密/解密
        val encrypt = cipher.doFinal(input.toByteArray())

        //base64加密
        return String(Base64.getEncoder().encode(encrypt))
    }

    //des解密
    fun decrypt(input:String,password:String): String {
        //1.创建cipher对象
        val cipher = Cipher.getInstance("DES")

        //2.初始化cipher(参数：加密/解密模式)
        val kf = SecretKeyFactory.getInstance("DES")
        val keySpec = DESKeySpec(password.toByteArray())

        val key: Key = kf.generateSecret(keySpec)
        cipher.init(Cipher.DECRYPT_MODE,key)

        //base64解码
        val encrypt = cipher.doFinal(Base64.getDecoder().decode(input))

        return String(encrypt)
    }
}

fun main(args: Array<String>) {

    val input = "DES加密解密测试"
    val password = "12345678"

    val encrypt = DESCrypt.encrypt(input,password)

    println("des加密="+encrypt)

    val decrypt = DESCrypt.decrypt(encrypt, password)

    println("des解密="+decrypt)

}
```
