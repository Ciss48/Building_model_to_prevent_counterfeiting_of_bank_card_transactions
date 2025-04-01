# Building_model_to_prevent_counterfeiting_of_bank_card_transactions
## Tổng quan ý tưởng
Đoạn code này thực hiện bài toán phát hiện gian lận giao dịch thẻ ngân hàng. Bài toán này thuộc dạng phát hiện bất thường (anomaly detection), trong đó giao dịch bình thường (class = 0) chiếm phần lớn, còn giao dịch gian lận (class = 1) rất ít.

Chính vì cách biệt quá lớn giữa giao dịch bình thường và giao dịch gian lận, ta không nên làm những mô hình phân loại bình thường

Ý tường của tôi là xây dựng mô hình tự mã hóa (Autoencoder) được sử dụng để học các mẫu giao dịch bình thường (class = 0). Mục tiêu: Autoencoder học cách tái tạo lại dữ liệu bình thường (class = 0) một cách tốt nhất. Nếu ta truyền 1 dữ liệu bình thường, nó sẽ tái tạo tốt. Nếu truyền dữ liệu bất thường (fraud) -> nó sẽ không tái tạo tốt, dẫn đến mức độ lỗi tái tạo (reconstruction error) cao. Dựa vào ngưỡng lỗi (threshold), nếu lỗi tái tạo quá cao, mô hình dự đoán đó là giao dịch gian lận.

Tại sao lại học từ giao dịch bình thường?
- Trong bài toán phát hiện gian lận, các giao dịch bình thường (class = 0) chiếm đa số (dữ liệu mất cân bằng).
- Autoencoder là mô hình học không giám sát (unsupervised), có nhiệm vụ nén dữ liệu rồi tái tạo dữ liệu.
- Nếu bạn đưa các giao dịch bình thường vào, mô hình sẽ học cách tái tạo lại đặc trưng của dữ liệu bình thường.
- Khi gặp giao dịch bất thường, do không có trong quá trình học, mô hình tái tạo kém, dẫn đến lỗi tái tạo cao.


