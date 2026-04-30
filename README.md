# social-media-marketing-performance-analytics
1, Bối cảnh và Lĩnh vực
Dự án này thuộc lĩnh vực Social Media Marketing Performance trong vai trò DA của 1 công ty IT toàn cầu, với mục tiêu phân tích dữ liệu hiệu suất nội dung truyền thông được triển khai trên nhiều nền tảng mạng xã hội nhằm tối ưu chiến lược nội dung và kênh phân phối. 
2, Vấn đề và bài toán cần giải quyết
Hiện tại, công ty đang triển khai nhiều loại nội dung (video, carousel, text, livestream…) trên các nền tảng khác nhau và hướng tới nhiều khu vực địa lý. Tuy nhiên, hiệu quả chiến dịch không đồng đều giữa nền tảng, loại nội dung, thời điểm đăng và khu vực. Vì vậy, bài toán đặt ra là:
Xác định các yếu tố (platform, post type, content category, hashtag, thời điểm đăng, khu vực địa lý) ảnh hưởng đến hiệu suất nội dung, từ đó đưa ra insights và recommendations, business actions phù hợp để cải thiện hiệu quả social media marketing (tối ưu engagement/views/clicks tùy mục tiêu).
3) Mục tiêu phân tích
Dựa trên dataset được cung cấp, mục tiêu của Big Project là:
1.	Đánh giá hiệu suất tổng quan theo từng nền tảng và loại nội dung: nền tảng nào/định dạng nào tạo ra engagement hoặc views tốt nhất. 
2.	Phân tích hiệu suất theo nội dung và khu vực: content category nào hiệu quả hơn ở các region/country khác nhau; có chênh lệch vùng miền về engagement/CTR không. 
3.	Tối ưu chiến lược đăng bài: xác định ngày/giờ đăng tối ưu để tối đa hoá engagement. 
4.	Đánh giá hashtag và loại phân phối (organic vs promoted): hashtag nào giúp tăng impressions/clicks; so sánh hiệu quả của phân loại marketing giữa organic và sponsored. 
4) Dữ liệu sử dụng (Dataset)
•	Nền tảng (ví dụ: TikTok, Instagram, LinkedIn, X.com…);
•	Metadata nội dung: post type (video/carousel/text), content category (product promotion/educational/entertainment…), thời điểm đăng (ngày/giờ), hashtag;
•	Phạm vi địa lý: country/region;
•	Chỉ số hiệu suất: engagement, views, impressions, clicks, click-through rate (CTR), cùng các chỉ số Marketing khác.
Dataset này cho phép phân tích hiệu suất theo nhiều “chiều” (platform–content–time–geo) để trả lời các câu hỏi cốt lõi về “điều gì làm nội dung thành công trên từng nền tảng và từng khu vực”.
Phát biểu bài toán
A) OVERVIEW 
Mục tiêu (như HR overview): Cho Ban giám đốc/Marketing lead/Stakeholder nhìn nhanh hiệu suất tổng thể và biết nên đào sâu vào đâu.
A1. Khối lượng hoạt động
1.	Tổng cộng có bao nhiêu bài đăng trong toàn bộ dữ liệu?
2.	Số lượng bài được chia ra theo từng nền tảng (TikTok/Instagram/LinkedIn…) như thế nào?
3.	Trong từng nền tảng, các loại bài (video, ảnh, text, livestream…) chiếm tỷ trọng ra sao?
Ý nghĩa: nếu nền tảng A có nhiều bài hơn quá nhiều, thì tổng performance của nó sẽ lớn hơn là điều dễ hiểu ta cần nhìn vào cả chất lượng nữa.
A2. Hiệu quả tổng quan (cả về độ phủ sóng lẫn chất lượng)
4.	Tổng số Impressions / Views / Engagement là bao nhiêu?
5.	Mức Engagement Rate trung bình là bao nhiêu?
6.	Nếu dữ liệu có Click/CTR, thì tổng Click và CTR trung bình là bao nhiêu ?
Ý nghĩa: ở phần overview, ta muốn nhìn ở cả 2 mặt:
•	Độ phủ: nội dung được thấy nhiều không? (views/impressions)
•	Chất lượng: người xem có tương tác không? (engagement rate)
A3. So sánh nhanh giữa các nền tảng
7.	Nền tảng nào đứng đầu về Views/Impressions (tức là lan tỏa mạnh)?
8.	Nền tảng nào đứng đầu về Engagement Rate (tức là tương tác tốt)?
9.	Nếu có CTR: nền tảng nào kéo traffic(lưu lượng truy cập) tốt nhất?
Ý nghĩa: không phải nền tảng nào có lượng tiếp cận lớn cũng là nền tảng có chất lượng tốt. Overview giúp xác định “mạnh – yếu” ban đầu.
A4. Xu hướng theo thời gian & độ ổn định
10.	Hiệu quả có tăng/giảm theo thời gian không (theo tuần/tháng)?
11.	Có thời điểm nào performance tăng vọt hoặc giảm mạnh không?
12.	Performance có bị phụ thuộc vào 1 số  postg viral không? (ví dụ top 1% bài tạo ra bao nhiêu % tổng views/engagement)
Ý nghĩa: nếu vài bài top kéo tất cả lên, chiến lược của ta nên tập trung vào công thức bền vững, chứ không phụ thuộc vào sự may mắn.
B) DETAIL 1 – Đào sâu theo “Nền tảng + Nội dung”
Mục tiêu: Từ overview đi xuống: Hiệu suất khác nhau là do platform nào và nội dung nào?
B1. Loại bài nào hiệu quả nhất trên từng nền tảng?
1.	Với mỗi nền tảng, loại bài nào (video/ảnh/text/live) có Engagement Rate tốt nhất?
2.	Với mỗi nền tảng, loại bài nào tạo Views/Impressions tốt nhất?
3.	Nếu có CTR: với mỗi nền tảng, loại bài nào tạo CTR tốt nhất?
Ý nghĩa: một loại bài có thể hợp TikTok nhưng không hợp LinkedIn. Đây là phần giúp ta đưa recommendation cho đúng kênh – đúng format.
B2. Chủ đề nội dung nào hiệu quả nhất?
4.	Content Category nào có Engagement Rate cao nhất?
5.	Content Category nào có Views/Impressions cao nhất?
6.	Content Category nào vừa có reach tốt vừa có chất lượng tốt? ( không chỉ nhiều views mà còn có ER hiệu quả )
Ý nghĩa: có thể có category kéo reach tốt ( có thế mạnh viral/entertainment), có category lại kéo chất lượng tốt (hướng tới educational/community). Ta cần phân vai rõ ràng.
B3. Kết hợp Platform + Post Type + Category
7.	Combo nào là tối ưu: nền tảng nào + loại bài nào + category nào thường cho kết quả tốt?
8.	Có combo nào không nên làm nhiều hoặc cần điều chỉnh lại vì hiệu quả thấp nhưng đang chiếm tỷ trọng lớn không?
Ý nghĩa: Giúp ta đưa ra được các chiến lược lựa chọn nền tảng, phương thức và lựa chọn danh mục phù hợp hơn, tăng cường phát triển và phát huy điểm mạnh, loại bỏ bớt và cải tạo lại điểm yếu.
C) DETAIL 2 – Đào sâu theo “Thời điểm đăng” (Time / Publishing Strategy)
Mục tiêu: Tìm kiếm giờ vàng/ngày vàng, kiểm tra tính mùa vụ, và tối ưu lịch đăng. 
C1. Ngày nào trong tuần hiệu quả hơn?
1.	Engagement Rate theo từng ngày trong tuần ra sao?
2.	Views/Impressions theo từng ngày trong tuần ra sao?
3.	Nếu có CTR: CTR theo ngày trong tuần ra sao?
Ý nghĩa: Tìm kiếm ngày đăng bài hiệu quả, có đầu ra tốt
C2. Khung giờ nào hiệu quả hơn?
4.	Engagement Rate theo giờ đăng (Post_Hour) ra sao?
5.	Views theo giờ đăng ra sao?
6.	Nếu có CTR: CTR theo giờ đăng ra sao?
C3. “Giờ vàng” có khác theo từng nền tảng không?
7.	Giờ vàng của TikTok có giống giờ vàng của LinkedIn không?
8.	Nếu khác nhau, lịch đăng nên tách theo nền tảng như thế nào?
Ý nghĩa: Hầu hết các team đăng một lịch cho tất cả. Data thường cho thấy mỗi nền tảng sẽ có nhịp riêng của nó.
C4. Độ ổn định của giờ vàng
9.	Giờ vàng có ổn định theo nhiều tuần/tháng không hay chỉ tốt trong 1 giai đoạn?
10.	Nếu không ổn định, ta có nên coi đó là gợi ý tạm thời thay vì quy tắc cố định không?
D) DETAIL 3 – Đào sâu theo “Khu vực + Hashtag + Organic/Promoted”
Mục tiêu: Tìm insight theo khu vực/nhóm khách hang và yếu tố  tăng trưởng như hashtag & sponsered/organic.
D1. Phân tích theo khu vực 
1.	Region/Country nào có Engagement Rate cao nhất?
2.	Region/Country nào có Views/Impressions cao nhất?
3.	Một loại nội dung (category) có hiệu quả giống nhau ở các region không, hay có nơi hợp nơi lại không hợp?
4.	Platform nào mạnh ở region nào? (ví dụ: LinkedIn mạnh ở khu vực A, TikTok mạnh ở khu vực B)
Ý nghĩa: Nếu doanh nghiệp có nhiều thị trường, thì chiến lược nội dung nên tùy biến phù hợp theo xu hướng và thị hiếu của người dùng theo khu vực.
D2. Phân tích hiệu quả hashtag
5.	Hashtag nào thường đi kèm với impressions/views cao hơn?
6.	Hashtag nào thường đi kèm với engagement rate cao hơn?
7.	Nếu có CTR: hashtag nào giúp kéo click tốt hơn?
8.	Có hashtag nào trông có vẻ tốt nhưng thực ra chỉ xuất hiện ở rất ít bài (ít mẫu) không?
Ý nghĩa: hashtag có thể tạo hiệu ứng tốt, nhưng nếu chỉ dựa vào 1–2 bài thì dễ kết luận sai. Ta cần nhìn cả tổng thể số lượng bài.
D3. So sánh Organic vs Sponsored
9.	Bài sponsored và bài organic khác nhau thế nào về views/impressions?
10.	Sponsored có làm Engagement Rate giảm không? Nếu có, mức giảm đó có đáng để đổi lấy reach/click không?
11.	Nếu có CTR: Sponsored có thật sự kéo CTR/click tốt hơn không?
Ý nghĩa: phần này giúp đưa ra recommendation khi nào nên chạy Sponsored, khi nào nên để organic.

