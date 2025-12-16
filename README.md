# CAFA6 – Dự đoán chức năng protein

## Giới thiệu
Dự án này thực hiện bài toán **Protein Function Prediction** trong khuôn khổ cuộc thi **CAFA6** trên Kaggle. Phương pháp chính bao gồm suy diễn dựa trên **tương đồng trình tự (DIAMOND)** kết hợp với các bước **hậu xử lý theo Gene Ontology**, đồng thời có thử nghiệm kết hợp với mô hình học máy.

Ngoài bộ dữ liệu chính do ban tổ chức CAFA6 cung cấp, dự án có **sử dụng thêm dữ liệu bên ngoài** nhằm mở rộng không gian tham chiếu và cải thiện chất lượng dự đoán.

## Các bộ dữ liệu bên ngoài được sử dụng

### 1. Dữ liệu CAFA5 bổ sung
Link:  
https://kaggle.com/datasets/26690474604463eb72530448b4399425fa8733ebbff0a88476aee6d9d87b816c

- Bao gồm các protein và nhãn Gene Ontology từ cuộc thi **CAFA5**.
- Được sử dụng như **tập protein tham chiếu bổ sung** cho quá trình tìm kiếm tương đồng bằng DIAMOND.
- Giúp tăng độ phủ về mặt chức năng so với chỉ sử dụng dữ liệu CAFA6.

### 2. Dữ liệu UniProt (sequence + GO annotation)
Link:  
https://kaggle.com/datasets/e67c1fd08273fb181a022cc55fa9fd85bd401c26e03aacf98a8a80884d661eb2

- Cung cấp các chuỗi protein UniProt cùng với chú giải GO tương ứng.
- Đóng vai trò là **cơ sở tri thức sinh học quy mô lớn**, hỗ trợ suy diễn chức năng dựa trên tương đồng trình tự.
- Đặc biệt hữu ích trong các trường hợp protein kiểm tra không có họ hàng gần trong tập huấn luyện CAFA6.

## Mục đích sử dụng dữ liệu bên ngoài
Việc tích hợp hai bộ dữ liệu trên nhằm:
- Mở rộng tập protein tham chiếu cho DIAMOND.
- Tăng khả năng tìm thấy protein tương đồng về mặt tiến hóa.
- Cải thiện độ bao phủ và độ ổn định của các dự đoán GO, đặc biệt ở các nhãn hiếm.

Các dữ liệu bên ngoài **chỉ được sử dụng làm reference** cho quá trình suy diễn, **không sử dụng nhãn của tập kiểm tra CAFA6**, đảm bảo tuân thủ quy định của cuộc thi.

## Ghi chú
- Kết quả từ các nguồn dữ liệu khác nhau được kết hợp ở **mức điểm dự đoán** (score-level fusion).
- Sau khi hợp nhất, kết quả được hậu xử lý bằng **lan truyền theo phân cấp Gene Ontology** để đảm bảo tính nhất quán sinh học.
