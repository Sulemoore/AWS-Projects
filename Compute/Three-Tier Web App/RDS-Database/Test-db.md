## Testing the database

- Copy Database endpoint
- Chnage directory to:
```
cd /vat/www/html/phpMyAdmin
```
- Rename  `Config.sample.Inc.php` to 'Config.Inc.php'

```
mv Config.sample.Inc.php Config.Inc.php
```

- Open the text editor, locate the `hostname` and replace it with the database endpoint
```
vi config.Inc.php
```
- Save and quit (:wq!)

### Test Site

- Copy ALb endpoint and append `phpMyAdmin' and test tour site. You should get:

![Screenshot 2023-09-02 at 11 46 29 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/6d9ff196-1229-423f-bbc5-10b23ac4328f)

- Login with the username and password you set for the Database at conffiguration.

![Screenshot 2023-09-02 at 11 46 52 PM](https://github.com/Sulemoore/AWS-Projects/assets/101164153/edf6390e-4dc3-426a-99ef-9cb2445cb924)
