# ITsec_TLS
傳輸層安全協定

TLS 提供了安全可靠的點對點通訊服務，可應用於電商購物車與線上結帳等等，利用特殊的封包封裝資料，讓 HTTPs 取代 HTTP，讓伺服器應用程式和客戶端應用程式能夠在超文本傳輸中，預設為 TLS，保障其傳輸安全。



                          HTTP
                            |
                           TLS
                            |
                           TCP
                           
                           
                           
                            |
                          IPsec
                            
                          

1. 確認 - 買家客戶需要確定對應的伺服器是真正的賣主。

2. 完整 - 買賣家之間的訊息需要確定未被竄改，而且完整。

3. 機密 - 買家傳送給賣家的個人資訊包含信用卡授權碼未被中間人攔截。

# TLS 技術

TLS 設計對來自於應用層產生的資要提公壓縮服務，其服務協定範圍仍然在 HTTP，能接收來自應用層協定的傳輸資料，收到資料時，會將其壓縮、簽署、加密，然後傳到 TCP 協定通道中。

