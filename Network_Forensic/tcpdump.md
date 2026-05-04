# Tcpdump Fundamentals

**Tcpdump** သည် Command-line ပေါ်တွင် Network Traffic များကို ဖမ်းယူရန်နှင့် စစ်ဆေးရန်အတွက် အားအကောင်းဆုံး Tool တစ်ခုဖြစ်ပါတယ်



### Basic Capture Options

| **Switch**         | **ဖော်ပြချက် (Result)**                                      |
| ------------------ | ------------------------------------------------------------ |
| **-D**             | Capture လုပ်လို့ရတဲ့ Interface စာရင်းအားလုံးကို ပြပေးပါတယ်။            |
| **-i [interface]** | ဖမ်းယူမည့် Interface ကို ရွေးချယ်ပေးရပါတယ်။ (ဥပမာ- `-i eth0`)    |
| **-n**             | IP address တွေနဲ့ Port နံပါတ်တွေကို နာမည်အဖြစ် မပြောင်းလဲဘဲ နံပါတ်အတိုင်းပဲ ပြပါတယ်။ (ပိုမြန်စေပါတယ်) |
| **-e**             | Upper-layer data တွေနဲ့အတူ Ethernet Header ကိုပါ ဖမ်းယူပြသပေးပါတယ်။ |
| **-X**             | Packet တစ်ခုချင်းစီရဲ့ ပါဝင်အချက်အလက်တွေကို **Hex** နှင့် **ASCII** ပုံစံနှစ်မျိုးလုံးဖြင့် ပြသပေးပါတယ်။ |
| **-XX**            | `-X` နှင့် တူသော်လည်း Ethernet headers များကိုပါ အသေးစိတ် ပြသပေးပါတယ်။ |
| **-v, -vv, -vvv**  | Output ထွက်လာတဲ့အခါမှာ အသေးစိတ်အချက်အလက် (Verbosity) ဘယ်လောက်ပါဝင်ရမလဲဆိုတာ တိုးမြှင့်သတ်မှတ်တာပါ။ |
| **-c [number]**    | Packet အရေအတွက် အတိအကျကို ဖမ်းယူပြီးတာနဲ့ Program ကို ရပ်လိုက်စေချင်တဲ့အခါ သုံးပါတယ်။ |
| **-s [size]**      | Packet တစ်ခုချင်းစီရဲ့ ဘယ်လောက်ပမာဏ (Size) ကို ဖမ်းယူမလဲဆိုတာ သတ်မှတ်ပေးပါတယ်။ |
| **-S**             | Relative sequence numbers အစား အမှန်တကယ်ရှိတဲ့ **Absolute sequence numbers** တွေကို ပြသခိုင်းတာပါ။ |
| **-q**             | Protocol အချက်အလက်တွေကို အကျဉ်းချုပ် (လျော့နည်းစွာ) ပြသပေးပါတယ်။ |
| **-r [file.pcap]** | သိမ်းဆည်းထားပြီးသား PCAP ဖိုင်တစ်ခုကို ပြန်လည်ဖတ်ရှု (Read) ဖို့ သုံးပါတယ်။ |
| **-w [file.pcap]** | ဖမ်းယူရရှိတဲ့ Traffic တွေကို ဖိုင်တစ်ခုထဲသို့ သိမ်းဆည်း (Write) ရန် သုံးပါတယ်။ |



## Tcpdump Output

![](/home/zane001/Pictures/Screenshots/breakdown.png)

| **အရောင်**      | **အစိတ်အပိုင်း**           | **ရှင်းလင်းချက်**                                            |
| --------------- | ----------------------- | ------------------------------------------------------------ |
| **အဝါရောင်**    | **Timestamp**           | Packet ကို ဖမ်းယူရရှိသော အချိန်နှင့် နေ့စွဲ ဖြစ်ပါသည်။ ၎င်းကို မိမိဖတ်ရလွယ်သော ပုံစံသို့ ပြောင်းလဲသတ်မှတ်နိုင်သည်။ |
| **လိမ္မော်ရောင်** | **Protocol & IP.Port**  | အသုံးပြုထားသော Upper-layer protocol (ဥပမာ- IP) နှင့် ပေးပို့သူ/လက်ခံသူတို့၏ IP နှင့် Port နံပါတ်များကို ဖော်ပြသည်။ (ဥပမာ- `172.16.146.2.21`) |
| **အစိမ်းရောင်**  | **Flags**               | TCP Flag များကို ပြသခြင်း ဖြစ်သည် (ဥပမာ- `[P.]` သည် PUSH flag ကို ဆိုလိုသည်)။ |
| **အနီရောင်**     | **Seq & Ack Numbers**   | TCP segment များကို ခြေရာခံရန် အသုံးပြုသော Sequence နှင့် Acknowledgment နံပါတ်များ ဖြစ်သည်။ |
| **အပြာရောင်**   | **Protocol Options**    | Window size ကဲ့သို့သော Client နှင့် Server ကြား ညှိနှိုင်းထားသည့် TCP တန်ဖိုးများကို ပြသသည်။ |
| **အဖြူရောင်**    | **Notes / Next Header** | ပရိုဂရမ်မှ ခွဲခြမ်းစိတ်ဖြာတွေ့ရှိသည့် အခြားအချက်အလက်များ ဖြစ်သည်။ ပုံပါနမူနာတွင် FTP traffic ဖြစ်ကြောင်း ဖော်ပြထားသည်။ |

---

### Tcpdump Packet Filtering

##### အခြေခံ Filter များ

- **host**: သတ်မှတ်ထားသော host နှင့် သက်ဆိုင်သည့် အဝင်/အထွက် traffic အားလုံးကို ပြသပေးသည်။

- **src / dest**: ၎င်းတို့သည် ပြုပြင်မွမ်းမံသည့် modifiers များဖြစ်ပြီး သတ်မှတ်ထားသော source (မူလအစ) သို့မဟုတ် destination (ဦးတည်ရာ) host/port ကို သီးသန့် ရွေးချယ်နိုင်သည်။

- **net**: သတ်မှတ်ထားသော network (ဥပမာ- `/` notation အသုံးပြုထားသော network segment) မှ လာသော သို့မဟုတ် သွားသော traffic များကို ပြသသည်။

- **proto**: သီးသန့် protocol အမျိုးအစား (ဥပမာ- ether, TCP, UDP, ICMP) များကို စစ်ထုတ်ပေးသည်။

- **port**: သတ်မှတ်ထားသော port နံပါတ်ကို source သို့မဟုတ် destination အဖြစ် အသုံးပြုထားသည့် traffic များကို ပြသသည်။

- **portrange**: သတ်မှတ်ထားသော port အကွာအဝေး (ဥပမာ- 0-1024) အတွင်းရှိ traffic များကို ပြသသည်။

- **less / greater ("< >")**: packet ပမာဏ သို့မဟုတ် protocol option ၏ အရွယ်အစားကို သတ်မှတ်၍ ရှာဖွေရာတွင် အသုံးပြုသည်။

- **and / &&**: မတူညီသော filter နှစ်ခုကို ပေါင်းစပ်ရန် အသုံးပြုသည် (ဥပမာ- `src host AND port`)။

- **or/ ||**: ပေးထားသော အခြေအနေနှစ်ခုအနက် တစ်ခုခုနှင့် ကိုက်ညီလျှင် ပြသပေးသည်။

- **not**: သတ်မှတ်ထားသော အချက်မှလွဲ၍ ကျန်ရှိသည်များကို ပြသရန် အသုံးပြုသည် (ဥပမာ- `not UDP`)။

  

##### Host Filter #####

```shell-session
 sudo tcpdump -i eth0 host 172.16.146.2
```

##### Source/Destination Filter

```shell-session
sudo tcpdump -i eth0 src host 172.16.146.2
sudo tcpdump -i eth0 dst host 172.16.146.2
```

##### Utilizing Source With Port as a Filter

```shell-session
sudo tcpdump -i eth0 tcp src port 80
sudo tcpdump -i eth0 tcp dst port 80
```

##### Using Destination in Combination with the Net Filter

```shell-session
 sudo tcpdump -i eth0 dst net 172.16.146.0/24
 sudo tcpdump -i eth0 src net 172.16.146.0/24
```

##### Protocol Filter - Common Name

```shell-session
sudo tcpdump -i eth0 udp
sudo tcpdump -i eth0 tcp
sudo tcpdump -i eth0 icmp
```

##### Protocol Filter - Number | tcp[6], udp[17], or icmp[1]

```shell-session
sudo tcpdump -i eth0 proto 17
```

##### Port Range Filter

```shell-session
sudo tcpdump -i eth0 portrange 0-1024
```

##### Less/Greater Filter

```shell-session
sudo tcpdump -i eth0 less 64
sudo tcpdump -i eth0 greater 500
```

##### AND Filter

```shell-session
sudo tcpdump -i eth0 host 192.168.0.1 && port 23
```

##### OR FIlter

```shell-session
sudo tcpdump -r sus.pcap icmp  host 172.16.146.1
```

##### NOT Filter

```shell-session
sudo tcpdump -r sus.pcap not icmp
```



**Absolute Sequence Numbers:** `-S` switch ကို အသုံးပြုပါက absolute sequence numbers များကို ပြသမည်ဖြစ်ပြီး ၎င်းတို့သည် အလွန်ရှည်လျားသော ဂဏန်းများဖြစ်နိုင်သည်။

**Relative Sequence Numbers:** ပုံမှန်အားဖြင့် tcpdump သည် relative sequence numbers များကို ပြသပေးလေ့ရှိပြီး ၎င်းတို့သည် ခြေရာခံရန်နှင့် ဖတ်ရှုရန် ပိုမိုလွယ်ကူသည်။

**Cross-tool Tracking:** အကယ်၍ tcpdump မှ packet တစ်ခုကို အခြား log သို့မဟုတ် tool တစ်ခုတွင် ပြန်လည်ရှာဖွေလိုပါက absolute sequence numbers ကိုသာ အသုံးပြု၍ ရှာတွေ့နိုင်မည်ဖြစ်သည်။ ဥပမာ - `13245768092588` ကဲ့သို့သော ဂဏန်းသည် relative အနေဖြင့် `100` ဟုသာ ပြသနေနိုင်သည်။

**ဒေတာတိုးမြှင့်ခြင်း:** `-v`, `-X`, နှင့် `-e` switch များသည် ဖမ်းယူရရှိသော ဒေတာပမာဏကို တိုးမြှင့်ပေးနိုင်သည်။

**ဒေတာလျှော့ချခြင်းနှင့် ပြုပြင်ခြင်း:** `-c`, `-n`, `-s`, `-S`, နှင့် `-q` switch များသည် ရေးသားသော သို့မဟုတ် မြင်တွေ့ရသော ဒေတာပမာဏကို လျှော့ချရန်နှင့် ပြုပြင်ရန် ကူညီပေးသည်။

**ASCII သီးသန့်ကြည့်ရှုခြင်း:** `-A` switch သည် packet line ပြီးနောက် ASCII စာသားကိုသာ ပြသပေးမည်ဖြစ်ပြီး Hex များကို ပြသမည်မဟုတ်ပါ။

**Line Buffering:** `-l` switch သည် tcpdump ကို output ထုတ်ရာတွင် mode ပြောင်းလဲစေပြီး ဒေတာများကို စုပြုံ၍ (pooling) ပို့မည့်အစား တစ်ကြောင်းချင်းစီ (line buffer) ပို့ဆောင်ပေးသည်။

**Piping to Grep:** `-l` ကို အသုံးပြုခြင်းဖြင့် tcpdump မှထွက်လာသော output ကို `grep` ကဲ့သို့သော အခြား tool များသို့ pipe (`|`) သုံး၍ တိုက်ရိုက်ပေးပို့နိုင်စေသည်။



##### Human Readable Stings Filter

```shell-session
sudo tcpdump -Ar telnet.pcap
```

##### Specific Strings Filter

```shell-session
sudo tcpdump -Ar http.cap -l | grep 'mailto:*'
```

##### Looking for TCP Protocol Flags

```shell-session
sudo tcpdump -i eth0 'tcp[13] &2 != 0'
```

##### Hunting For a SYN Flag

```shell-session
sudo tcpdump -i eth0 'tcp[13] &2 != 0'
```