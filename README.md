# QoS

### 1. Phân loại hàng đợi

First-in First-out (FIFO): Đây là cơ chế hàng đợi đơn giản nhất, gói tin được đưa vào một hàng đợi và được xử lý theo trình tự nhận được. Trong thiết kế của thiết bị, người ta coi mỗi hàng đợi riêng lẻ là một hàng đợi FIFO, các cơ chế phát triển sau này đều là từ FIFO mà ra, chỉ khác nhau về thứ tự lấy bản tin ra từ các hàng đợi để xử lý.

<p align="center"><img src="https://github.com/ajino2k/QoS/blob/master/fifo_queue1.png"></center></p>

- Priority Queue (PQ): PQ sử dụng nhiều hàng đợi FIFO. Gói tin đi vào sẽ được classify và đánh dấu ưu tiên. Dựa vào giá trị này, gói tin sẽ được đưa vào các hàng đợi có độ ưu tiên tương ứng. Thiết bị sẽ xử lý hết các gói tin trong hàng đợi có độ ưu tiên cao hơn, sau đó mới xử lý đến các hàng đợi có độ ưu tiên thấp.

<p align="center"><img src="https://github.com/ajino2k/QoS/blob/master/priority_queue1.png"></p/

- Weighted Round Robin (WRR): WRR sử dụng nhiều hàng đợi FIFO, mỗi hàng đợi được gán một trọng số ưu tiên (weight). Hàng đợi nào có trọng số ưu tiên hơn sẽ được gửi nhiều gói tin hơn theo tỷ lệ tương ứng giữa các hàng đợi. VD: Hàng đợi 1 (Q1) có 5 gói tin đang chờ, hàng đợi 2 (Q2) có 3 gói tin đang chờ. Set weight của Q1 = 4, weight của Q2 = 2 => Thiết bị sẽ lấy ra 4 gói tin trong Q1, sau đó lấy ra 2 gói tin trong Q2, cứ thế cho đến hết gói tin.

<p align="center"><img src="https://github.com/ajino2k/QoS/blob/master/weighted_round_robin_queue2.png"></p>

### 2. Cơ chế chống tắc nghẽn trong hàng đợi

## 2.1. Cơ chế tail-drop

- Khi hàng đợi đầy hoặc bắt đầu quá tải, các gói tin đến sẽ bị drop cho đến khi nào hàng đợi được giải phóng. Trong TCP và UDP, tail-drop gây ra hiện tượng Global Synchronization và TCP Starvation.

## 2.2. Cơ chế RED (Random Early Detection)

- RED hạn chế tắc nghẽn trong hàng đợi bằng cách loại bỏ ngẫu nhiên một số gói tin đang có trong hàng đợi khi hàng đợi đầy. Để làm được điều này, RED cần xử lý 2 vấn đề:

- Khi nào bắt đầu loại bỏ gói tin?
- Và loại bỏ bao nhiêu gói tin là đủ?
