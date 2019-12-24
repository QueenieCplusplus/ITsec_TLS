# ITsec_TLS
傳輸層安全協定

TLS 提供了安全可靠的點對點通訊服務，可應用於電商購物車與線上結帳等等，利用特殊的封包封裝資料，讓 HTTPs 取代 HTTP，讓伺服器應用程式和客戶端應用程式能夠在超文本傳輸中，預設為 TLS，保障其傳輸安全。

ISO

                           HTTP
                            |
                           TLS
                            |
                           TCP
                           
                           
                           
                            |
                          IPsec
                            

# TLS 技術

TLS 設計對來自於應用層產生的資要提公壓縮服務，其服務協定範圍仍然在 HTTP，能接收來自應用層協定的傳輸資料，收到資料時，會將其壓縮、簽署、加密，然後傳到 TCP 協定通道中。

1. 完整 <- 對收到的資料進行分割與壓縮，而接收端則會接收並重組。

2. 確認 <- 利用 MD5 或是 SHA-1 建立 MAC Signature。

            MAC means "Message Authentication Code"

3. 機密 <- 標頭裝框在加密後的 loader 中，此 loader 也會被傳送到 TCP 傳輸協定中，而接收方則會進行去框，得到標頭內文。
>>>

             Client       < - >     R/W   < - >        Server
             
             Write means Sign & Send
             Read means Verif & Receive
>>>

1. 確認 -> 買家客戶需要確定對應的伺服器是真正的賣主。

2. 完整 -> 買賣家之間的訊息需要確定未被竄改，而且完整。

3. 機密 -> 買家傳送給賣家的個人資訊包含信用卡授權碼未被中間人攔截。


TLS

                        三方交握
                             \
                              \
                            伺服器確認和金鑰交換
                                \
                                 \
                                用戶確認和金鑰交換
                                   \
                                    \
                                    完成與結束
                                 

>>>
ServerKeyExchange

             
             Client                        Server
                                             /
                                            /
                                       憑證鏈（表明自己身份）
                                          /
                                 伺服器公開金鑰藉此交換金鑰
                                        /
                                 請求憑證
                                     /
                           伺服器端完成（無內容）                                            

>>>
ClientKeyExchange

             Client                        Server
                \
                 \
                憑證鏈（表明自己身份）
                   \
                   用戶端公開金鑰藉此交換金鑰
                     \
                     用 Hash code 證明憑證
                    
>>>
ChanegCipherSpec

               Client                       Server
                 ｜                            
                  ---- 密文變更值 ---------->      |
                   ----  MD5+SHA ---------->    |
                       <----------密文變更值----|
                       <----------MD5+SHA----|             
                     


# Session & Connection, 會議與連線

又稱會議連線，會議的意思是用戶端和伺服器端的連結，然而連結可能不安全，故需要建立安全的連線。一個會議可能由很多連線所建立，兩者之間的連線也可以被終止，也能在相同會議下重建，也就是說一個會議的連線能在終止後再次恢復。

建立新會議，需要 TCP 重新協商過程，然而如果上述的連線是從舊的 session 恢復連線的話，則可略過 TCP 三方交握的過程，直接進行連線，節省寶貴的時間。

# Session Options, 會議的參數

   Session ID
   
   https://github.com/QueenieCplusplus/Backend_Script2/tree/master/PhpSession-master
   
   https://github.com/QueenieCplusplus/Backend_Script2/blob/master/PhpSession-master/Session.php
   
   Peer Cert (X.509)
   
   Compress
   
   Crypto (雙方均同意的加密套件，見 ChangeCipherSpec Protocol)
   
   Key (48 bytes 的 value)

# Connection Options, 連線的參數


             Client       <->     R/W R/W   <->      Server
                          <->     R/W R/W   <-> 
                          <->     R/W R/W   <-> 
          
             3 pair of Keys means there are 6 R/W Keys

   Random
   
   MAC key
   
   key
   
   Init Vector in CBC
   
   https://github.com/QueenieCplusplus/ITsec_BeastCrime#beast--crime
   
   Seq
   
# Connection Verify by 3way Hand Shake, 三方交握
   
Header
   
        Protocol:22        Version:          Length:
        Type:       

Protocol

        20 密文變更協定
        21 警示協定，報告異常或致命。
        22 握手協定
        23 來自應用層資料
 
Type

         0  HelloReq
         1  ClientHello
         2  ServerHello
        11  Cert
        12  ServerKeyExchange
        13  CertReq
        14  ServerHelloDone
        15  CertVerify
        16  ClientKeyExchange
        20  Fisnished  
   
# TCP

 https://github.com/QueenieCplusplus/Networking/blob/master/TCP.md
   
   
