# tool_gen_data_nlu

```
text = "tôi thích ăn cơm"
gen_data = "tôi thích ăn mì quảng", "tôi thích ăn phở"
```
ta thấy các từ cơm , mì quảng , phở tại trong loại data này có dạng đồng nghĩa và entity của nó là món ăn
ta có thể xây dựng cáu trúc câu kiểu 
- tôi thích ăn [slot]
slot : cơm, mì quảng, phở
nhưng dạng trên chỉ có thể thay thế 1
ta cần có thể gen data được nhiều câu có nhiều slot