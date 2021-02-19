# 前置作業
- 基於Windows 10，配合書內容的筆記
- 安裝bochs
    - bochs就是個純軟體實踐的虛擬機，效能因為沒有硬體優化，所以普普，但在超多系統上都可以用，下載網址 : 
    [https://sourceforge.net/projects/bochs/](https://sourceforge.net/projects/bochs/)
    - 安裝的時候記得把DLX Linux Demo打勾，這樣他就會產生一個default 的linux image，不用再自己建一個
    - 安裝好後打開bochs會自動啟動DLX Linux這個os，並要求登入，使要帳號打root，不用密碼就可以登了
        [Running the DLX Linux Demo on Bochs](https://minix1.woodhull.com/faq/rundlx.html)

- 學組語
    教學網站
    [Assembly 指示符_w3cschool](https://www.w3cschool.cn/assembly/assembly-Indicator.html)
	
- 第一、二章的內容 : 
	- 首先要建立虛擬機的環境，bochs建立虛擬機的方式是先把虛擬機的config寫好，副檔名是.bxrc，config太多要填了，  
	  我就不自己做一個，直接copy前置作業的DLX Linux的config，稍作修改就行了
		1. 先進到bochs的安裝路徑 C:\Program Files\Bochs-2.6.11，這裡面就包含所有虛擬機要用到的東西了，包含虛擬機config裡有些要讀的檔站路徑也是這個資料夾，    
		裡面有個資料夾是dlxlinux，進去有個bochsrc.bxrc就是DLX Linux的config了
		2. 我就模仿dlxlinux自己建一個helloworld的虛擬機，把config丟進去吧
		3. 我需要自己做一個開機碟模仿MBR，照書裡的步驟用C:\Program Files\Bochs-2.6.11裡的bximage.exe建立一個floppy disk image
		4. 把MBR的assembly code寫好，用nasm轉成bin檔(就是機器語言)，指令 : nasm boot.asm -o boot.bin
		   nasm下載網址 : https://www.nasm.us/pub/nasm/releasebuilds/2.15.05/win64/
		5. 把bin檔寫進剛剛建的image裡，課本裡說用rawrite，但windows好像不支援，可以用一個工具叫dd for windows : http://www.chrysocome.net/dd  
		   他就是linux的dd指令做成windows版本，下指令 : dd if=boot.bin of=a.img bs=512 count=1  
		   課本裡面還有參數 conv=notrunc，但dd for windows好像不支援，就不理他了
		6. 修改config讓他拿掉原本的disk掛載新寫好的disk image(詳細改了什麼看commit就知道)
		7. 模仿dlxlinux建一個run.bat小改一下，跑這個bat就可以了~~~可以看一下bat裡面在幹嘛