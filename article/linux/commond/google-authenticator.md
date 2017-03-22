## 安装Google Authenticator
Google Authenticator开源版主页 [https://github.com/google/google-authenticator](https://github.com/google/google-authenticator)

### 安装Google Authenticator

**Ubuntu**已经包含libpam-google-authenticator软件(Ubuntu 11.10以上版本),可以直接使用`apt-get`安装

```shell
apt-get install libpam-google-authenticator
```

其他系统可以通过源码编译安装

```shell
git clone https://github.com/google/google-authenticator.git
cd google-authenticator/libpam/
./bootstrap.sh
./configure
make
make install
```

注意：在Debian7中执行`./configure`时可能存在以下错误提示

```
configure: error: Unable to find the PAM library or the PAM header files
```

在此需要安装`libpam0g-dev`和`libtool`

```shell
apt-get -y install libpam0g-dev libtool
```

### 设置Google Authenticator

在手机端搜索安装**Google Authenticator**

```
google-authenticator
Do you want authentication tokens to be time-based (y/n) y
```

然后出现二维码，使用手机端**Google Authenticator**扫码,接下来服务器端继续设置

```shell
Do you want me to update your "/root/.google_authenticator" file (y/n) y

Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, tokens are good for 30 seconds and in order to compensate for
possible time-skew between the client and the server, we allow an extra
token before and after the current time. If you experience problems with poor
time synchronization, you can increase the window from its default
size of 1:30min to about 4min. Do you want to do so (y/n) y

If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting (y/n) y
```

接下来将**Google Authenticator**验证配置到SSH登录中

编辑`/etc/pam.d/sshd`文件，添加下行保存

```shell
auth required pam_google_authenticator.so #/usr/local/lib 目录下找找
```

编辑`/etc/ssh/sshd_config`找到下行

```shell
ChallengeResponseAuthentication no
```

更改为

```shell
ChallengeResponseAuthentication yes
```

重启SSH服务

```shell
service ssh restart
```

再次登录的话输入用户名后就跟着提示两部验证码，然后才输入用户密码，如下：

```
login as: root
Using keyboard-interactive authentication.
Verification code:
Using keyboard-interactive authentication.
Password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 2.6.32-042stab108.8 i686)

* Documentation:  https://help.ubuntu.com/
Last login: Thu Jan 28 15:04:20 2016 from 61.185.216.146
root@hkvps:~#
```