# tool_gen_data_nlu

```
text = "tôi thích ăn cơm"
gen_data = "tôi thích ăn mì quảng", "tôi thích ăn phở"
```
* ta thấy các từ cơm , mì quảng , phở tại trong loại data này có dạng đồng nghĩa là món ăn.
* ta có thể xây dựng cáu trúc câu kiểu 
  - tôi thích ăn [slot]

  slot : cơm, mì quảng, phở
  với m giá trị thay thế 1 slot ta có thể tạo m câu tương tự,ở đây m = 2
  
### **Trong thực tế** :
  *ta cần có thể gen data thành nhiều câu với nhiều slot ví dụ như* 
```
text = " tôi thích đi du lịch ở Hội An vì nơi đó có món mì quảng rất ngon "
gen_data = "tôi thích đi du lịch ở Hà Nội vì nơi đó có món Phở rất ngon", "tôi thích đi du lịch ở Huế vì nơi đó có món bánh bèo Huế rất ngon"
```
* ta thấy rõ ràng khi gen ta cần 2 slot với cấu trúc kiểu
  - tôi thích đi du lịch ở [slot] vì nơi đó có món [slot] rất ngon.
* để slot slot ta rất khó phân biệt slot gì thay thế từ gì nên dựa vào **NER** (**Named Entity Recognition**) ta có thể thay thế cấu trúc thành 
  - tôi thích đi du lịch ở [location] vì nơi đó có món [food] rất ngon.
  - như vậy ta có thể thấy với m location và n food thì ta sẽ có m * n các câu gen nhưng nó lại không chắc có ý nghĩa chính xác.
  
### = > vậy bài toán ta đặt ra là có thể tạo ra đủ nhiều data tương ứng:
  * **Số Lượng** :
  - với 1 slot là m từ đồng nghĩa sẽ gen được m câu
  - với nhiều slot thì tương ứng data gen sẽ tăng theo cấp số nhân ví dụ 2slot : slot 1 có m từ , slot 2 có n từ tổng cộng sẽ là m * n câu được gen
  * **Ngữ nghĩa** :
  - TH1 : bắt buộc ngữ nghĩa.ta cần chú ý số lượng câu gen ra sẽ theo cấp số cộng và cấp số nhân kết hợp với nhau
  ```
  ví dụ lấy ở trên câu "tôi thích đi du lịch ở [location] vì nơi đó có món [food] rất ngon"
  location Hà Nội => food : phở,bún,bún riêu cua,phở Hà,bún đậu mắm tôm ở đây food = 5
  location Huế => food : bún Huế,bún bò Huế,cơm hến,bánh bèo,bánh bột lọc ở đây food = 5
  ta có 2 location và 10 food nhưng số câu gen ra chỉ là 1 * 5 + 1 * 5 vì lý do mỗi 1 location đi kèm chỉ có 5 food mà không phải 10.nên kết quả là 10 mà không phải 20.
  ```
  - TH2 : không bắt buộc ngữ nghĩa. vậy ta cần bao nhiêu câu gen chỉ cần có số lượng slot và số từ đồng nghĩa tương ứng với mỗi slot tương ứng
  ```
  ví dụ như sau : tôi muốn mua [object] có màu [color] giá [price]
  object : quần,áo,mũ,giày,dép
  color: xanh lá, đỏ,đen,xanh dương
  price: 100k,200k,500k,1tr
  thì số câu ta có thể gen ra là 5 * 4 * 4 = 80 câu 
  ```
  **qua đó ta muốn gen data ra bao nhiêu câu thì cần xem xét số lượng slot và số lượng từ đồng nghĩa, đồng thời yêu cầu suy tính ngữ cảnh có thích hợp hay không để có thể gen ra đủ sô lượng data và đủ chất lượng**
  
