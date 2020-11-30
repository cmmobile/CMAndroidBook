# Overview

## 為什麼要使用

如果我們在Main Thread執行費時的工作或是API的請求，將會造成Main Thread被主塞，導致App被凍結。所以必須將這些工作移至其他Thread執行，而Coroutine是一個簡單管理非同步的操作。不像被棄用的AsyncTask或是直接產生一個新的Thread，這些工作如果要取消，都要做複雜的操作。

## Callback vs Coroutine

情境：現在使用者要輸入帳號密碼登入我們的伺服器，最後會得到使用者相關數據。

### Callback

```text
class LoginViewModel(){
    fun login(){
        //don't do this in prodcut code
        task1 = thread {
            respority.login(account, password, object: Callback<User> {
                fun onSuccess(user: User) {}
                fun onFailure(exceptione: Exception) {}
            })
        }
    }
    
    onCleared(){
        task1.cancel()
    }
}

class Respority {
    fun login(account: String, password: String, result: Callback<User>) {
        //do some connection
        if(task is successful) {
            result.onSuccess(user)
        } else {
            result.onFaliure(exception)
        }
    }
}
```

### Coroutine

```text
sealed class Result<out R> {
    data class Success<out T>(val data: T) : Result<T>()
    data class Error(val exception: Exception) : Result<Nothing>()
}

class LoginViewModel(){
    fun login(){
        viewModelScope.launch(Dispatchers.IO) {
            val loginResult = login(account, password)
            if (loginResult is Result.Success<User>) {
            
            } else {
            
            }
        }
    }
}

class Respority {
    suspend fun login(account: String, password: String): Result<User> {
        //do some connection
        if(task is successful) {
            return Result.Success(user)
        } else {
            return Result.Error(exception)
        }
    }
}
```

Let's dissect the coroutines code in the `login` function:

* `viewModelScope` 是一個預先定義在`ViewModel`KTX擴展方法的`CoroutineScope` 。所有的Coroutines都必須在一個Scope內執行。一個`CoroutineScope` 管理一個或多個相關的Coroutines。
* `launch` 是一個創造Coroutine和分配方法的內容會在哪一個對應的Dispatchers執行的方法。
* `Dispatchers.IO` 暗示這個Coroutine應該在I/O Thread被執行。

## 參考

[官方簡介](https://developer.android.com/kotlin/coroutines)

