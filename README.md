# Tiki E-Commerce Data Analysis and Visualization

Đây là repository nộp bài cuối kỳ môn **Phân Tích và Trực Quan Hóa Dữ Liệu**. Dự án phân tích bộ dữ liệu thương mại điện tử Tiki tại Việt Nam, tập trung vào nhóm sản phẩm **Fashion & Accessories**.

Nhóm thực hiện phân tích dữ liệu, làm sạch dữ liệu, trực quan hóa, kiểm định giả thuyết và xây dựng mô hình hồi quy để tìm hiểu các yếu tố liên quan đến hành vi bán hàng trên Tiki.

## Thành viên nhóm

| MSSV | Họ và tên | Phân công chính | Hoàn thành |
|---|---|---|---|
| 52300135 | Lê Quang Hồng Ngọc | Data understanding, data cleaning review, final category, presentation preparation and report writing support. | 100% |
| 52300138 | Nguyễn Trí Nhân | Gender-oriented analysis, interpretation of shoes and bags behavior, notebook integration, pipeline synchronization, visualization organization, LaTeX/IEEE report preparation. | 100% |
| 52300143 | Nguyễn Lai Vũ Phong | BNPL research design, Pay Later analysis, revenue-proxy interpretation, brand-level BNPL visualization, hypothesis framing. | 100% |

## Chủ đề phân tích

Dự án được xây dựng quanh 3 hướng nghiên cứu chính:

1. **Pay Later / BNPL**

   Phân tích vai trò của `pay_later` để xem đây chủ yếu là công cụ hỗ trợ các sản phẩm giá cao hay là yếu tố kích thích nhu cầu mua hàng rộng hơn. Nhóm so sánh sản phẩm có và không có BNPL theo `quantity_sold`, phân khúc giá và cấu trúc doanh thu ước lượng.

2. **Rating paradox**

   Kiểm tra hiện tượng sản phẩm có điểm đánh giá tuyệt đối 5.0 chưa chắc bán tốt hơn nhóm sản phẩm có điểm 4.7-4.9 nhưng có nhiều đánh giá hơn. Phần này nhấn mạnh vai trò của social proof thông qua `review_count`.

3. **Gender behavior trong Shoes và Bags**

   So sánh hành vi sản phẩm hướng đến nam và nữ trong hai nhóm `Shoes` và `Bags`, bao gồm giá, khuyến mãi, số lượng đánh giá, tốc độ bán và hình thức giao hàng. Việc xét đồng thời cả giày và túi giúp tránh kết luận thiên lệch từ một danh mục đơn lẻ.

## Cấu trúc repository

| File | Mô tả |
|---|---|
| `52300135_52300138_52300143.ipynb` | Notebook chính chứa toàn bộ pipeline phân tích dữ liệu, từ đọc dữ liệu, làm sạch, EDA, kiểm định giả thuyết đến hồi quy tuyến tính bội. |
| `52300135_52300138_52300143_Report.pdf` | Báo cáo cuối kỳ theo định dạng học thuật, trình bày bối cảnh, phương pháp, kết quả phân tích và kết luận. |
| `52300135_52300138_52300143_Presentation.pdf` | Slide thuyết trình tóm tắt nội dung và kết quả chính của dự án. |
| `.gitattributes` | Thiết lập Git để tự động nhận diện text files và chuẩn hóa line endings. |

## Dataset

Nguồn dữ liệu: [Vietnamese Tiki E-Commerce Dataset](https://www.kaggle.com/datasets/michaelminhpham/vietnamese-tiki-e-commerce-dataset)

Notebook sử dụng 6 file CSV thuộc nhóm thời trang và phụ kiện:

- `vietnamese_tiki_products_men_bags.csv`
- `vietnamese_tiki_products_women_bags.csv`
- `vietnamese_tiki_products_men_shoes.csv`
- `vietnamese_tiki_products_women_shoes.csv`
- `vietnamese_tiki_products_backpacks_suitcases.csv`
- `vietnamese_tiki_products_fashion_accessories.csv`

Sau khi gộp dữ liệu, notebook làm việc với **41,603 bản ghi** và bổ sung các biến như `main_category`, `target_gender`, `discount_percent`, `sales_velocity`, `price_segment`, `pay_later_int`, `has_video_int`, `is_tiki_delivery` để phục vụ phân tích.

Do giới hạn dung lượng và bản quyền dữ liệu, các file CSV gốc không được lưu trực tiếp trong repository này. Để chạy lại notebook, tải dữ liệu từ Kaggle và đặt các file CSV vào thư mục:

```text
./dataset/
```

Nếu chạy bằng Google Colab, notebook cũng hỗ trợ đọc dữ liệu từ Google Drive qua đường dẫn được cấu hình trong phần đầu notebook.

## Quy trình phân tích trong notebook

Notebook được tổ chức theo các phần:

1. **Setup & Load**

   Import thư viện, cấu hình đường dẫn dữ liệu, đọc 6 file CSV, kiểm tra schema và gộp dữ liệu.

2. **Data Cleaning & Feature Engineering**

   Kiểm tra missing values, loại sản phẩm trùng theo `id`, loại sản phẩm có giá bằng 0, phát hiện outlier bằng IQR và tạo biến phục vụ 3 chủ đề nghiên cứu.

3. **Exploratory Data Analysis**

   Trực quan hóa phân bố danh mục, giá, rating, review, Pay Later, doanh số, delivery type và các khác biệt theo giới tính/danh mục.

4. **Probability Distribution**

   Phân tích phân phối biến `price`, dùng histogram, KDE, Q-Q plot và KS test. Kết quả cho thấy log transformation phù hợp hơn do dữ liệu giá bị lệch phải.

5. **Hypothesis Testing**

   Dùng Mann-Whitney U test cho các giả thuyết về BNPL, rating paradox và khác biệt giới tính trong từng nhóm sản phẩm.

6. **Correlation Analysis**

   Phân tích tương quan Spearman và trực quan hóa các cặp biến quan trọng.

7. **Multiple Linear Regression**

   Xây dựng mô hình hồi quy tuyến tính bội với biến phụ thuộc `log_qty_sold`, kiểm tra VIF, đánh giá mô hình và phân tích phần dư.

## Kết quả chính

- `pay_later` có liên hệ rõ với sản phẩm giá cao và cấu trúc doanh thu theo thương hiệu, nhưng không nên hiểu đơn giản là yếu tố làm tăng trực tiếp số lượng bán.
- Nhóm sản phẩm rating 4.7-4.9 nhưng có nhiều review có thể thuyết phục người mua tốt hơn nhóm rating 5.0 nhưng ít review.
- Phân tích theo giới tính cần được kiểm chứng trên nhiều danh mục. Shoes và Bags cho thấy một số khác biệt không nên được khái quát hóa nếu chỉ nhìn vào một nhóm sản phẩm.
- Trong mô hình hồi quy, `log_review_count` là biến dự báo mạnh nhất cho `log_qty_sold`, củng cố vai trò của social proof.
- `log_price` có hệ số âm, cho thấy giá cao thường đi kèm lượng bán thấp hơn sau khi kiểm soát các biến khác.
- `is_tiki_delivery` và `has_video_int` có tác động tích cực, gợi ý rằng độ tin cậy giao hàng và nội dung trình bày sản phẩm hỗ trợ hiệu quả bán hàng.

## Cách chạy notebook

1. Tải dataset từ Kaggle.
2. Tạo thư mục `dataset` tại gốc repository.
3. Đặt 6 file CSV vào thư mục `dataset`.
4. Mở `52300135_52300138_52300143.ipynb` bằng Jupyter Notebook, JupyterLab hoặc Google Colab.
5. Chạy lần lượt các cell từ đầu đến cuối.

Các thư viện Python chính được sử dụng:

- `numpy`
- `pandas`
- `matplotlib`
- `seaborn`
- `scipy`
- `statsmodels`

## Tài liệu nộp kèm

- Báo cáo cuối kỳ: `52300135_52300138_52300143_Report.pdf`
- Slide thuyết trình: `52300135_52300138_52300143_Presentation.pdf`
- Notebook phân tích: `52300135_52300138_52300143.ipynb`
