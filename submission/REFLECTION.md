# Reflection

Trên 50 query, Hybrid đạt Precision@10 cao nhất với 78,6%, so với BM25
77,8% và Vector 73,2%. Với nhóm `exact`, BM25 và Hybrid cùng đạt 96,7% vì
các từ khóa kỹ thuật xuất hiện trực tiếp trong tài liệu. Với nhóm
`paraphrase`, kết quả lần lượt là BM25 33,3%, Vector 24,0% và Hybrid 32,0%;
điều này cho thấy model `bge-small-en-v1.5` chưa tối ưu cho tiếng Việt. Với
nhóm `mixed`, Hybrid thắng với 100% nhờ kết hợp tín hiệu từ khóa và ngữ nghĩa
bằng RRF.

Tôi không dùng Hybrid khi chỉ cần khớp chính xác mã, tên biến hoặc thuật ngữ,
vì pure BM25 đơn giản và ít độ trễ hơn. Pure Vector phù hợp với query hoàn
toàn mang tính ngữ nghĩa nếu embedding model hỗ trợ tốt ngôn ngữ dữ liệu.
Hybrid là lựa chọn an toàn cho truy vấn thực tế có tính pha trộn.

Điều bất ngờ nhất là warm-up ảnh hưởng rõ đến P99: Hybrid ban đầu vượt 50 ms,
nhưng sau warm-up P99 còn khoảng 15 ms. PIT join cũng cho thấy dữ liệu tương
lai không được sử dụng, giúp tránh data leakage.

Tôi đã hoàn thành bốn notebook cốt lõi NB1–NB4 theo Lite path. GitHub Copilot
hỗ trợ đọc code, giải thích TODO và phân tích output; tôi chịu trách nhiệm
chạy notebook, kiểm tra kết quả và chuẩn bị ảnh minh chứng. Chưa làm bonus
challenge.
