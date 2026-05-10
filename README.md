# Termius-cracked

## Метод взлома был проверен в версии 9.6.1

Установите npm. Установите asar.
```shell
npm config set registry http://mirrors.cloud.tencent.com/npm/
npm install -g @electron/asar
```

### for Windows
1. Распакуйте app.asar
```shell
cd C:\Users\[XXXXX]\AppData\Local\Programs\Termius\resources
npx asar extract app.asar ./app
rm app-update.yml  # Предотвратить автоматические обновления
```

### for MAC

1. Распакуйте app.asar
```shell
cd /Applications/Termius.app/Contents/Resources/
npx asar extract app.asar ./app
rm app-update.yml  # Предотвратить автоматические обновления
```

### Измените js

#### Измените app/background-process/assets/main-xxxxxxx.js

Найдите `await this.api.bulkAccount`

`const e=await this.api.bulkAccount();` -> `var e=await this.api.bulkAccount();`

```js
var e=await this.api.bulkAccount();
e.account.pro_mode=true;
e.account.need_to_update_subscription=false;
e.account.current_period={
    "from": "2022-01-01T00:00:00",
    "until": "2099-01-01T00:00:00"
};
e.account.plan_type="Premium";
e.account.user_type="Premium";
e.student=null;
e.trial=null;
e.account.authorized_features.show_trial_section=false;
e.account.authorized_features.show_subscription_section=true;
e.account.authorized_features.show_github_account_section=false;
e.account.expired_screen_type=null;
e.personal_subscription={
    "now": new Date().toISOString().slice(0, -5),
    "status": "SUCCESS",
    "platform": "stripe",
    "current_period": {
        "from": "2022-01-01T00:00:00",
        "until": "2099-01-01T00:00:00"
    },
    "revokable": true,
    "refunded": false,
    "cancelable": true,
    "reactivatable": false,
    "currency": "usd",
    "created_at": "2022-01-01T00:00:00",
    "updated_at": new Date().toISOString().slice(0, -5),
    "valid_until": "2099-01-01T00:00:00",
    "auto_renew": true,
    "price": 12.0,
    "verbose_plan_name": "Termius Pro Monthly",
    "plan_type": "SINGLE",
    "is_expired": false
};
e.access_objects=[{
    "period": {
        "start": "2022-01-01T00:00:00",
        "end": "2099-01-01T00:00:00"
    },
    "title": "Pro"
}]
return .......
```
3. Запустите Termius, войдите в свою учетную запись и перезапустите Termius.


### Ручная синхронизация нескольких устройств
Win：C:\Users\[XXXXX]\AppData\Roaming\Termius\IndexedDB\file__0.indexeddb.leveldb\000003.log
Mac：/Users/[XXXXX]/Library/Application Support/Termius/000003.log
