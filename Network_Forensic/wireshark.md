#                    Analysis with Wireshark

### Basic TShark Switches

| **Switch**         | **ဖော်ပြချက် (Result)**                                      |
| ------------------ | ------------------------------------------------------------ |
| **-D**             | Capture ပြုလုပ်နိုင်သည့် interface စာရင်းအားလုံးကို ပြသပြီးနောက် ပရိုဂရမ်မှ ထွက်ပါမည်။ |
| **-L**             | Capture ပြုလုပ်နိုင်သည့် Link-layer mediums (ဥပမာ - ethernet) စာရင်းကို ပြသပါမည်။ |
| **-i [interface]** | Traffic ဖမ်းယူမည့် interface ကို ရွေးချယ်ရန်ဖြစ်သည်။ (ဥပမာ - `-i eth0`)။ |
| **-f [filter]**    | Libpcap syntax ကိုအသုံးပြု၍ capture ပြုလုပ်နေစဉ်အတွင်း packet များကို စစ်ထုတ်ရန်ဖြစ်သည်။ |
| **-c [number]**    | သတ်မှတ်ထားသော packet အရေအတွက် ပြည့်ပါက program ကို ရပ်တန့်စေရန်ဖြစ်သည်။ |
| **-a [condition]** | Autostop condition သတ်မှတ်ရန်ဖြစ်သည်။ အချိန်ကြာမြင့်မှု (duration)၊ ဖိုင်ဆိုဒ် သို့မဟုတ် packet အရေအတွက်ပေါ် မူတည်၍ ရပ်တန့်စေနိုင်သည်။ |
| **-r [file]**      | သိမ်းဆည်းထားသော pcap file ကို ပြန်လည်ဖတ်ရှုရန်ဖြစ်သည်။           |
| **-W [file]**      | Traffic များကို **pcapng** format ဖြင့် ဖိုင်ထဲသို့ ရေးသားသိမ်းဆည်းရန်ဖြစ်သည်။ |
| **-P**             | ဖိုင်ထဲသို့ သိမ်းဆည်းနေစဉ် ( -W သုံးနေစဉ်) တစ်ပြိုင်နက်တည်းမှာပင် packet summary များကို terminal ပေါ်တွင် ပြသပေးရန်ဖြစ်သည်။ |
| **-x**             | Capture ပြုလုပ်ရာတွင် Hex နှင့် ASCII output များကိုပါ ထည့်သွင်းပြသရန်ဖြစ်သည်။ |
| **-h**             | Help menu ကို ကြည့်ရှုရန်ဖြစ်သည်။                                |



##### Selecting an Interface & Writing to a File

```shell-session
sudo tshark -i eth0 -w /tmp/test.pcap
```

##### Applying Filters

```shell-session
sudo tshark -i eth0 -f "host 172.16.146.2"
```

---

### TERMSHARK

Terminal window ပေါ်တွင် တိုက်ရိုက်အသုံးပြုနိုင်သည့် Text-based User Interface (TUI) application တစ်ခုဖြစ်ပြီး **Wireshark** ၏ အလုပ်လုပ်ပုံနှင့် ဆင်တူသော interface မျိုး

![](/home/zane001/Pictures/Screenshots/termshark.png)

---

### Wireshark GUI Walkthrough

![](/home/zane001/Pictures/Screenshots/wireshark-menu.png)



### The Tool Bar

![](/home/zane001/Pictures/Screenshots/wireshark-toolbar.jpg)

### Capture Filters

| **Filter**                          | **ရလဒ် (Result)**                                            |
| ----------------------------------- | ------------------------------------------------------------ |
| **host x.x.x.x**                    | သတ်မှတ်ထားသော host နှင့် သက်ဆိုင်သည့် traffic များကိုသာ ဖမ်းယူသည်။  |
| **net x.x.x.x/24**                  | Slash notation ကို အသုံးပြု၍ သတ်မှတ်ထားသော network တစ်ခုလုံး၏ အဝင်/အထွက် traffic များကို ဖမ်းယူသည်။ |
| **src/dst net x.x.x.x/24**          | သတ်မှတ်ထားသော network မှ ထွက်လာသော (src) သို့မဟုတ် သွားမည့် (dst) traffic များကိုသာ သီးသန့်ဖမ်းယူသည်။ |
| **port #**                          | သင်သတ်မှတ်ထားသော port နံပါတ်မှလွဲ၍ ကျန်ရှိသော traffic အားလုံးကို ဖယ်ထုတ်ပစ်မည်။ |
| **not port #**                      | သတ်မှတ်ထားသော port မှလွဲ၍ ကျန်ရှိသော traffic အားလုံးကို ဖမ်းယူမည်။  |
| **port # and #**                    | **AND** operator ကို အသုံးပြု၍ သတ်မှတ်ထားသော port နှစ်ခုလုံး၏ traffic များကို ပေါင်းစပ်ဖမ်းယူသည်။ |
| **portrange x-x**                   | သတ်မှတ်ထားသော port အကွာအဝေးအတွင်းရှိ traffic များကိုသာ ဖမ်းယူမည်။ |
| **ip / ether / tcp**                | ၎င်းတို့သည် သတ်မှတ်ထားသော protocol headers များမှ traffic ကိုသာ ဖမ်းယူပေးမည်။ |
| **broadcast / multicast / unicast** | သီးသန့် traffic အမျိုးအစားများ (တစ်ဦးချင်း၊ အုပ်စုလိုက် သို့မဟုတ် အားလုံးသို့ ပေးပို့ခြင်း) ကို စစ်ထုတ်ဖမ်းယူသည်။ |



### Filter List

![](/home/zane001/Pictures/Screenshots/capture-filter-list.png)

### Applying A Capture Filter

![](/home/zane001/Pictures/Screenshots/how-to-add-cap.png)



### Display Filter

| **Filter**                     | **ရလဒ် (Result)**                                            |
| ------------------------------ | ------------------------------------------------------------ |
| **ip.addr == x.x.x.x**         | သတ်မှတ်ထားသော IP နှင့် သက်ဆိုင်သည့် (Source သို့မဟုတ် Destination ဖြစ်စေ) traffic များကို ပြသသည်။ (OR statement ကဲ့သို့ အလုပ်လုပ်သည်) |
| **ip.addr == x.x.x.x/24**      | သတ်မှတ်ထားသော network segment တစ်ခုလုံးနှင့် သက်ဆိုင်သည့် traffic များကို ပြသသည်။ |
| **ip.src / ip.dst == x.x.x.x** | သတ်မှတ်ထားသော host မှ ထွက်လာသော သို့မဟုတ် ၎င်းသို့ သွားမည့် traffic ကို သီးသန့်စစ်ထုတ်သည်။ |
| **dns / tcp / ftp / arp / ip** | သီးသန့် protocol အမျိုးအစားအလိုက် စစ်ထုတ်ကြည့်ရှုနိုင်သည်။              |
| **tcp.port == x**              | သီးသန့် TCP port နံပါတ်တစ်ခုတည်းကိုသာ ပြသရန်ဖြစ်သည်။               |
| **tcp.port / udp.port != x**   | သတ်မှတ်ထားသော port မှလွဲ၍ ကျန်ရှိသည်များကို ပြသသည်။              |
| **and / or / not**             | Logic operators များဖြစ်ပြီး Filter အများအပြားကို ပေါင်းစပ်ရန် (`and`)၊ တစ်ခုမဟုတ်တစ်ခု ရှာရန် (`or`) သို့မဟုတ် ဖယ်ထုတ်ရန် (`not`) အသုံးပြုသည်။ |



### Statistics Tab

ကွန်ရက်အတွင်း မည်သူတွေ အများဆုံး စကားပြောနေသလဲ၊ မည်သည့် protocol များကို အသုံးများသလဲဆိုသည်ကို အသေးစိတ် ပြသပေးသည်

**Conversations:** Host နှစ်ခုကြားက ဆက်သွယ်မှု (Handshake မှစ၍ အဆုံးအထိ) ကို အုပ်စုလိုက် ပြသပေးသည်။ ၎င်းသည် မည်သည့်စက်နှစ်ခုကြားတွင် ဒေတာ အများဆုံး ပေးပို့နေသလဲဆိုသည်ကို သိရှိရန် အကောင်းဆုံးဖြစ်သည်။

**Endpoints:** ကွန်ရက်အတွင်း ချိတ်ဆက်ထားသော စက်ပစ္စည်းတစ်ခုချင်းစီ၏ စာရင်းနှင့် ၎င်းတို့ ပေးပို့/လက်ခံခဲ့သော packet ပမာဏကို ပြသသည်။ "Top Talkers" များကို ဤနေရာတွင် ရှာဖွေနိုင်ပါသည်။

**Protocol Hierarchy:** ဖမ်းယူထားသော traffic ထဲတွင် မည်သည့် protocol (ဥပမာ- HTTP, TCP, UDP) က မည်မျှ ရာခိုင်နှုန်း ပါဝင်နေသည်ကို သစ်ပင်ပုံစံ (Tree view) ဖြင့် ပြသပေးသည်။



### Analyze Tab

 traffic များ၏ အဓိပ္ပာယ်ကို ပိုမိုနက်ရှိုင်းစွာ နားလည်စေရန် ကူညီပေးသည်

![](/home/zane001/Pictures/Screenshots/analyze.png)



**Follow (TCP/UDP/HTTP Stream):** Packet အစိတ်စိတ်အမွှာမွှာ ဖြစ်နေသည်များကို ပြန်လည်စုစည်းပြီး လူနားလည်နိုင်သော စာသားများ (ဥပမာ- Website တစ်ခု၏ HTML code သို့မဟုတ် Chat messages များ) အဖြစ် ပြသပေးသည်။

**Expert Information:** Wireshark မှ အလိုအလျောက် တွေ့ရှိထားသော ကွန်ရက်ဆိုင်ရာ အမှားအယွင်းများ (ဥပမာ- TCP Retransmissions, Checksum errors) ကို အဆင့်အလိုက် (Error, Warning, Note) ခွဲခြားပြသပေးသည်။

**အနီရောင် (Red):** Client ဘက်မှ Server သို့ ပေးပို့သော data များ (ဥပမာ - HTTP Request)။

**အပြာရောင် (Blue):** Server ဘက်မှ Client သို့ ပြန်လည်ဖြေကြားသော data များ (ဥပမာ - HTTP Response)။

![](/home/zane001/Pictures/Screenshots/follow-tcp.gif)



### Extract Files From The GUI

![](/home/zane001/Pictures/Screenshots/extract-http.gif)



### FTP Disector

![](/home/zane001/Pictures/Screenshots/ftp-disector.png)



### FTP-Request-Command Filter

`ftp.request.command` ဟု ရိုက်ထည့်လိုက်ပါက Client ဘက်မှ Server သို့ ပေးပို့လိုက်သော commands အားလုံးကို မြင်တွေ့ရမည်ဖြစ်ပြီး အောက်ပါတို့ကို အသေးစိတ် စစ်ဆေးနိုင်ပါသည် -

- **Usernames:** `USER` command နောက်တွင် လိုက်ပါလာသော အသုံးပြုသူအမည်။
- **Passwords:** `PASS` command နောက်တွင် လိုက်ပါလာသော စာဝှက်မထားသော စကားဝှက်။
- **Filenames:** `RETR` (Retrieve - ဖိုင်ရယူခြင်း) သို့မဟုတ် `STOR` (Store - ဖိုင်တင်ခြင်း) commands များတွင် ပါဝင်သော ဖိုင်အမည်များ။

![](/home/zane001/Pictures/Screenshots/ftp-request-command.png)

### FTP-Data Filter

`ftp-data` filter ကို အသုံးပြုခြင်းဖြင့် ကွန်ရက်အတွင်း အပြန်အလှန် ပေးပို့နေသော ဖိုင်များကို ဖမ်းယူနိုင်ပါသည်။

![](/home/zane001/Pictures/Screenshots/ftp-data.png)