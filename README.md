# XMRig

##【以下是我改动的文档】

XMRig-C3pool猫池去捐赠抽水版本-可自己编译版


##【相对于官方的改动如下】

src/donate.h 文件的 kMinimumDonateLevel和kDefaultDonateLevel修改为0

src/net/strategies/DonateStrategy.cpp 文件中 donate_user 捐赠地址改为自己的xmr钱包地址（编译时自己改为自己的即可），其实这里不改也行，只是改个安心

/src/base/net/stratum/Pools.cpp中158行的猫池域名判断语句删除，并加一句直接赋值mo = true; 使得判断条件永远为真


##【我编译好的版本】

* **[Binary releases](https://github.com/xinvhost/xmrig-C3/releases/)**

u16：在ubuntu16上编译（建议选择此版本，兼容性好，已测试兼容：ubuntu16+,debian10+,centos7+）

u22:在ubuntu22上编译（已测试兼容ubuntu22+,debian11,其他系统自行测试是否可以运行）

懒人直接运行以下命令下载解压

wget https://github.com/xinvhost/xmrig-C3/releases/xmrig-c3-u16.tar.gz && tar -zxvf xmrig-c3-u16.tar.gz

然后修改config.json文件中的参数：

url：矿池或矿池代理的地址和端口，user：xmr钱包地址，pass：当前客户端的显示名称，显示在矿池的矿机列表里，max-threads-hint：最大CPU使用率百分比，99就是99%，越大CPU使用的越多，background：是否后台运行，默认为true,则会自动在后台运行，log-file：日志文件名和路径

修改完成后，运行 chmod +x xmrig-c3 && sudo ./xmrig-c3 即可开始挖矿

日志查看 tail -f xmrig-c3.log ,如果改了日志路径和文件名，此处需对应


* 如果想自己编译的话以下是【编译步骤】：

建议在ubuntu16上编译以兼容低版本的系统（兼容性好）

推荐ubuntu20，也可以在其他ubuntu版本上编译，或者在其他linux发行版编译

注意：高版本的系统编译的二进制文件可能无法在低版本的系统上运行，另外编译过程中可能会出现报错，到时请根据错误提示进行环境的安装修复即可正常编译

sudo apt install git build-essential cmake automake libtool autoconf

git clone https://github.com/xinvhost/xmrig-C3.git

cd xmrig-C3/


去掉捐赠：

编辑src/donate.h 文件的 kMinimumDonateLevel和kDefaultDonateLevel修改为0

编辑src/net/strategies/DonateStrategy.cpp 文件中 donate_user地址改为自己的xmr钱包地址

编辑src/base/net/stratum/Pools.cpp中158行的域名判断语句删除，并加一句直接赋值mo = true;


在 xmrig-C3/目录下执行以下命令

mkdir build && chmod -R +x ./ && cd scripts 

./build_deps.sh && cd ../build

cmake .. -DXMRIG_DEPS=scripts/deps

如果此处报错，大概率是使用的低版本的系统编译使得openssl版本不兼容，可进入目录xmrig-C3/scripts/执行./build.openssl.sh安装openssl 1版本，完成后进入xmrig-C3/build/再执行cmake .. -DXMRIG_DEPS=scripts/deps 完成后再执行后面的编译命令
make -j$(nproc)

编译完后检查依赖是否正确 ldd xmrig

完成后可在xmrig-C3/build/看到编译好的 xmrig 文件。


##【编译参数】如果有特殊需求，可参考：https://xmrig.com/docs/miner/cmake-options



【以下是官方xmrig-c3的官方文档】


XMRig is a high performance, open source, cross platform RandomX, KawPow, CryptoNight and [GhostRider](https://github.com/xmrig/xmrig/tree/master/src/crypto/ghostrider#readme) unified CPU/GPU miner and [RandomX benchmark](https://xmrig.com/benchmark). Official binaries are available for Windows, Linux, macOS and FreeBSD.

## Mining backends
- **CPU** (x86/x64/ARMv7/ARMv8)
- **OpenCL** for AMD GPUs.
- **CUDA** for NVIDIA GPUs via external [CUDA plugin](https://github.com/C3Pool/xmrig-cuda).

## Download
* **[Binary releases](https://github.com/C3Pool/xmrig/releases)**
* **[Build from source](https://xmrig.com/docs/miner/build)**

## Usage
The preferred way to configure the miner is the [JSON config file](https://xmrig.com/docs/miner/config) as it is more flexible and human friendly. The [command line interface](https://xmrig.com/docs/miner/command-line-options) does not cover all features, such as mining profiles for different algorithms. Important options can be changed during runtime without miner restart by editing the config file or executing [API](https://xmrig.com/docs/miner/api) calls.

* **[Wizard](https://xmrig.com/wizard)** helps you create initial configuration for the miner.
* **[Workers](http://workers.xmrig.info)** helps manage your miners via HTTP API.

## Donations
* Default donation 1% (1 minute in 100 minutes) can be increased via option `donate-level` or disabled in source code.
* XMR: `48edfHu7V9Z84YzzMa6fUueoELZ9ZRXq9VetWzYGzKt52XU5xvqgzYnDK9URnRoJMk1j8nLwEVsaSWJ4fhdUyZijBGUicoD`

## Developers
* **[xmrig](https://github.com/xmrig)**
* **[sech1](https://github.com/SChernykh)**

## Contacts
* support@xmrig.com
* [reddit](https://www.reddit.com/user/XMRig/)
* [twitter](https://twitter.com/xmrig_dev)
