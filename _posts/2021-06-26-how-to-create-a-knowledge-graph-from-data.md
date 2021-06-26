---
layout: post
toc: true
comments: true
---
# ĐỒ THỊ TRI THỨC - KNOWLEDGE GRAPH

Đây là bản dịch từ Course CS520: Knowledge Graphs | Data Models, Knowledge Acquisition, Inference and Applications

Department of Computer Science, Stanford University, Spring 2021

Knowledge graphs have emerged as a compelling abstraction for organizing world's structured knowledge over the internet, capturing relationships among key entities of interest to enterprises, and a way to integrate information extracted from multiple data sources. Knowledge graphs have also started to play a central role in machine learning and natural language processing as a method to incorporate world knowledge, as a target knowledge representation for extracted knowledge, and for explaining what is being learned. This class is a graduate level research seminar and will include lectures on knowledge graph topics (e.g., data models, creation, inference, access) and invited lectures from prominent researchers and industry practitioners. The seminar emphasizes synthesis of AI, database systems and HCI in creating integrated intelligent systems centered around knowledge graphs.

Mục đích: Là tìm hiểu cũng như trau dồi kiến thức chuyên môn trong lĩnh vực Knowledge Graph cũng như từ vựng tiếng Anh. Không vì mục đích kinh doanh hay bất cứ mục đích về lợi nhuận, tất cả là vì mục đích chia sẻ kiến thức và học tập.

Mọi thông tin về những chủ đề được note lại có thể tìm thấy ở đây:

https://web.stanford.edu/class/cs520/2020/notes/Table\_Of\_Contents.html

Video của các buổi seminar cũng được công khai trên địa chỉ Youtube:

https://www.youtube.com/playlist?list=PLDhh0lALedc5paY4N3NRZ3j\_ui9foL7Qc

Mọi vấn đề về dịch thuật, thuật ngữ xin để lại comment hoặc gửi về địa chỉ email: lenam.fithcmus@gmail.com với tiêu đề

\[ISSUES OF KG TRANSLATION\]

# HOW TO CREATE A KNOWLEDGE GRAPH FROM DATA

## 1\. Giới thiệu

Những tổ chức lớn tạo ra lượng lớn dữ liệu nội bộ và cũng tiêu thụ dữ liệu được tạo ra bởi các nhà cung cấp bên thứ ba (third party providers). Nhiều nhà cung cấp dữ liệu có được dữ liệu bằng cách xử lý nhưng nguồn phi cấu trúc, và đầu tư một nổ lực đáng kể trong việc cung cấp nó trong một dạng có cấu trúc cho việc sử dụng của người dùng. Để sử dụng hiệu quả những dữ liệu bên ngoài, nó phải liên quan tới dữ liệu bên trong công ty, Như tích hợp dữ liệu cho phép nhiều trường hợp sử dụng phổ biến như 360 view of a customer - góc nhìn 360 độ của khách hàng, fraud detection - phát hiện gian lận, risk assessment - đánh giá rủi ro, loan approval - phê duyệt khoản vay, .. Với chương này, chúng ta sẽ thảo luận vấn đề khởi tạo một đồ thị tri thức bằng cách tích hợp dữ liệu có sẵn từ những nguồn có cấu trúc. Chúng ta sẽ xem xét vấn đề của việc rút trích dữ liệu từ những nguồn dữ liệu phi cấu trúc trong chương tiếp theo :v

Khi kết hợp dữ liệu từ nhiều nguồn vào một đồ thị tri thức, chúng ta có thể thực hiện một số thiết kế sơ đồ như chúng ta đã thảo luận trong chương trước :v Chúng ta cũng bắt đầu mà không cần lược đồ vì việc tải dữ liệu bên ngoài thẳng vào như bộ ba vào một đồ thị tri thức rất dễ dàng. Thông thường, thiết kế ban đầu của lược đồ dựa trên trường hợp cụ thể mà người ta muốn giải quyết. Ở mức độ tồn tại ban đầu của lược đồ như thế, chúng ta phải quyết định các thành phần dữ liệu từ một nguồn dữ liệu mới nên được thêm vào đồ thị tri thức như thế nào. Điều này thường được biết đến là vấn đề schema mapping - vấn đề ánh xạ lược đồ. Hơn nữa, để liên hệ lược đồ của hai nguồn, chúng ta cũng phải giải quyết khả năng mà một thực thể trong dữ liệu đến (ví dụ như một Company) có thể đã tồn tại trong đồ thị tri thức của chúng ta. Vấn đề suy luận nếu hai thực thể trong dữ liệu có thể cùng là một thực thể trong thế giới thực được gọi là vấn đề record linkage - mẫu ghi liên kết. Vấn đề mẫu ghi liên kết cũng xuất hiện khi các nhà cung cấp dữ liệu bên thứ ba gửi những nguồn cấp dữ liệu mới (a new data feeds), và đồ thị tri thức của chúng ta phải được cập nhật (up-to-daye) với những nguồn dữ liệu mới này.

Trong chương này, chúng ta sẽ cùng thảo luận những tiếp cận hiện tại cho giải quyết vấn đề ánh xạ lược đồ và vấn đề mẫu ghi liên kết. Chúng ta sẽ nêu những thuật toán state-of-the-art và thảo luận về mức độ hiệu qủa của chúng trong những vấn đề của ngành :v

## 2\. Ánh xạ lược đồ - Schema Mapping

Ánh xạ lược đồ giả định rằng tồn tại một lược đồ mà sẽ được sử dụng cho viêc lưu trữ dữ liệu mới đến từ một nguồn khác. Ánh xạ lược đồ sau đó xác định những quan hệ và thuộc tính nào trong cơ sở dữ liệu đầu vào tương ứng với những thuộc tính và quan hệ trong đồ thị tri thức. Tồn tại những kỹ thuật cho bootstrapping schema mappings. Bootstrapped schema mappings có thể được điều chỉnh thông qua sự can thiệp của con người.

Chúng ta sẽ bắt đầu thảo luận về ánh xạ lược đồ bằng cách nêu ra một số thách thức và nhận định liệu chúng ta có nên chuẩn bị cho việc phần lớn quá trình này có thể thực hiện thủ công và tốn nhiều công sức. Sau đó, chúng ta mô tả một tiếp cận cho việc chỉ định ánh xạ giữa lược đồ nguồn đầu vào và lược đồ của đồ thị tri thức. Chúng ta sẽ kết thúc mục này bằng đề cập một vài kỹ thuật có thể được sử dụng cho bootstrap schema mapping.

### 2.1 Những thách thức với Ánh xạ lược đồ - Schema Mapping

Những thách thức chính trong tự động ánh xạ lược đồ

\- (1) Khó để hiểu lược đồ

\- (2) Độ phức tạp của việc ánh xạ

\- (3) Ít dữ liệu huấn luyện có sẵn

Chúng ta sẽ thảo luận chi tiết hơn những thách thức này

Lược đồ cơ sở dữ liệu quan hệ thương mại (Commercial relational database schemas) có thể rất lớn bao gồm hàng ngàn quan hệ và hàng vạn thuộc tính. Thỉnh thoảng, tên của những quan hệ và thuộc tính không có ngữ nghĩa (ví dụ, segment1, segment2 @@ ) mà không liên quan gì bản thân chúng với bất kỳ dự đoán tự động thực tế nào của ánh xạ.

Ánh xạ giữa lược đồ đầu vào và lược đồ trong đồ thị tri thức không phải lúc nào cũng đơn giản là ánh xạ 1-1 (one-to-one mapping). Ánh xạ có thể liên quan tới những tính toán, áp dụng logic kinh doanh và có những luật đặc biệt cho việc xử lý tình huống như là missing values. Nó trở thành một sự kỳ vọng quá cao đối với bất kỳ quá trình xử lý tự động nào suy diễn những phép ánh xạ phức tạp như vậy.

Cuối cùng, nhiều giải pháp ánh xạ tự động dựa trên các kỹ thuật Máy học (Machine Learning techniques) yêu cầu một lượng lớn dữ liệu huấn luyện để hoạt động một cách hiệu quả. Như lược đồ thông tin, bằng định nghĩa, nhỏ hơn nhiều dữ liệu bản thân nó, rất là viễn vong để kỳ vọng rằng chúng sẽ có một lượng lớn ánh xạ lược đồ sẵn có để một thuật toán ánh xạ có thể được huấn luyện.

### 2.2 Xác định Ánh xạ lược đồ - Specifying Schema Mapping

Trong phần này, chúng ta sẽ đề cập một phương pháp tiếp cận khả thi để xác định ánh xạ giữa nguồn dữ liệu đầu vào và một mục tiêu trong lược đồ đồ thị tri thức. Chúng ta sẽ lấy một ví dụ trong lĩnh vực dụng cụ nấu ăn. Chúng ta có thể tưởng tượng những nhà cung cấp khác nhau cung cấp các mặt hàng trên một trang thương mại điện tử (E-commerce site) có mong muốn tổng hợp và quảng bá đến khách hàng của họ. Chúng ta sẽ xem xét hai nguồn ví dụ và sau đó thêm vào lược đồ đồ thị tri thức để mà chúng ta sẽ định nghĩa các ánh xạ.

Chúng ta hiển thị một vài mãu dữ liệu từ nguồn dữ liệu đầu tiên trong một bảng quan hệ gọi là cookware. Nó có bốn thuộc tính: name, type, material, và price

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image1.png)

Cơ sở dữ liệu thứ hai được hiển thị bên dưới cho thấy danh sách những sản phẩn của một nhà sản suất. Trong trường hợp này, có nhiều bảng, một bảng ứng với một thuộc tính sản phẩm. Bảng *kind* xác định loại của mỗi sản phẩm. Bảng *base* xác định mỗi sản phẩm được làm từ kim loại ăn mòn -corrosible metal (nhôm - aluminum hoặc không gỉ - stainless), kim loại không ăn mòn - noncorrosible metal (sắt - iron hoặc thép - steel) hay thứ gì đó không phải kim loại (thủy tinh hoặc gốm - ceramic). Bảng coated xác định những sản phẩm này có phủ chống dính hay không (nonstick coatings). Bảng price cho thông tin về giá bán. Không có thông về vật liệu. Công ty được chọn không cung cấp thông tìn về kim loại được sử dụng trong mỗi sản phải. Lưu ý rằng, bản coated chỉ có những giá trị dương; những sản phẩm mà không có lớp phủ chống dính không được đề cặp đến.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image2.png)

Giả sử rằng lược đồ mong muốn cho đồ thị tri thức được biểu diễn như một đồ thị thuộc tính được cho ở bên dưới đây. Chúng ta có hai loại nút khác nhau: một cho sản phẩm - Product, và cái kia cho các nhà cung cấp – Supplier. Hai nút này liên kết với nhau bởi một mối quan hệ gọi là *has\_supplier*. Mỗi nút sản phẩm có những thuộc tính là “type” và “price”

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image3.png)

Để xác định lược đồ ánh xạ và để xử lý cụ thể, chúng ta sẽ sử dụng định nghĩa một bộ ba để mà một xử lý tương tự có thể áp dụng bất kể chúng ta sử dụng mô hình dữ liệu đồ thị thuộc tính hay mô hình RDF cho đồ thị tri thức. Với một đồ thị tri thức RDF, chúng sẽ cần phải khởi tạo IRI, tức một quá trình trực giao để liên hệ hai lược đồ, và ở đây chúng ta bỏ qua điều này. Những bộ ba mong muốn trong mục tiêu đồ thị tri thức được liệt kê bằng bảng dưới đây.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image4.png)Bất kỳ ngôn ngữ lập trình nào có thể dược sử dụng để biểu diễn ánh xạ. Ở đây, chúng ta chọn sử dụng Datalog để biểu diễn ánh xạ. Các luật dưới đây rất đơn giản. Các biến được biểu thị bằng cách sử dụng các chữ cái in hoa. Luật thứ ba thêm ràng buộc vender\_1 để chỉ ra nguồn dữ liệu.

knowledge\_graph(ID,type,Type) :- cookware(ID,TYPE,MATERIAL,PRICE)  
knowledge\_graph(ID,price,PRICE) :- cookware(ID,TYPE,MATERIAL,PRICE)  
knowledge\_graph(ID,has\_supplier,vendor\_1) :- cookware(ID,TYPE,MATERIAL,PRICE)

Kế đến, chúng ta xem xét những luật cho việc ánh xạ nguồn dữ liệu thứ hai. Những luật cũng khá là tương tự như những luật ánh xạ cho nguồn dữ liệu thứ nhất ngoài trừ là thông tin bây giờ thì đến từ hai bảng khác nhau trong nguồn dữ liệu

knowledge\_graph(ID,type,Type) :- kind(ID,TYPE)

knowledge\_graph(ID,price,PRICE) :- price(ID,PRICE)

knowledge\_graph(ID,has\_supplier,vendor\_2) :- kind(ID,TYPE)

Tổng quát mà nói, nó không hợp lý khi sử dụng lại các bộ định danh từ cơ sở dữ liệu nguồn, và chúng ta mong muốn là tạo ra những bộ định danh mới cho việc sử dụng trong đồ thị tri thức. Trong một số trường hợp, đồ thị tri thức có thể đã chứa những đối tượng tương đương với chúng trong dữ liệu được nhập. Chúng ta sẽ xem xét vấn đề này trong phần mẫu ghi liên kết - record linkage

### 2.3 Bootstrapping Schema Mapping

Như được đề cập ở phần 2.1, một tiếp cận hoàn toàn tự động để ánh xạ lược đồ đối mặt với rất nhiều khó khăn trong thực tế. Ở đây đề cập một công trình về bootrapping the schema mappings dựa trên nhiều kỹ thuật và xác nhận chúng bằng đầu vào con người. Những kỹ thuật Boostrapping cho ánh xạ lược đồ có thể được phân loại thành những loại sau đây:

\- (1) Linguistic matching - Kết hợp ngôn ngữ học

\- (2) Matching based on instances - Kết hợp dựa trên thể hiện

\- (3) Matching based on constraints - Kết hợp dựa trên ràng buộc

Những kỹ thuật ngôn ngữ học có thể được sử dụng trên tên của một thuộc tính hoặc trên những văn bản mô tả của một thuộc tính. Các tiếp cận đầu tiên và cũng rõ ràng nhất là kiểm tra tên của hai thuộc tính là bằng nhau hay không. Chúng ta có thể có một độ tin cậy cao trong so sánh bằng nếu những tên là IRIs. Thứ hai, chúng ta có thể chuẩn hoá tên bằng cách xử lý chúng thông qua một số kỹ thuật như stemming và kiểu tra tính bằng nhau. Lấy ví dụ, thông qua xử lý, chúng ta có thể kết luận ánh xạ của CName đến Customer Name. Thứ ba, chúng ta có thể kiểm tra ánh xạ dựa trên từ đồng nghĩa - synonyms (ví dụ như là: car và automobile) hoặc từ siêu nghĩa - hypernyms (ví dụ như là book và publication). Thứ tư, chúng ta có thể kiểm tra ánh xạ dựa trên những chuỗi con chung, phát âm chung, và cách mà những từ đó được phát âm. Và cuối cùng, chúng ta có thể kết hợp những mô tả của những thuộc tính thông qua những kỹ thuật ngữ nghĩa tương đồng (semantic similarity techniques). Ví dụ, một cách tiếp cận để rút trích những từ khoá từ phần mô tả và sau đó kiểm tra độ tương đồng giữa chúng bằng cách sử dụng những kỹ thuật mà chúng ta đã nếu ra.

Trong kết hợp dựa trên những thể hiện, người ta kiểm tra loại dữ liệu có tồn tại. Ví dụ, nếu một giá trị thuộc tính cụ thể mang kiểu dữ liệu ngày tháng, nó chỉ có thể kết hợp dựa trên những thuộc tính mang những giá trị ngày tháng. Nhiều kiểu dữ liệu chuẩn hoá có thể được suy diễn bằng cách kiểu tra dữ liệu

Trong một số trường hợp, lược đồ cung cấp thông tin về những ràng buộc. Ví dụ, nếu một lược đồ xác định một thuộc tính cụ thể là đơn nhất đối với một cá thể, và phải là số, nó là một đối sánh tiềm năng hoặc các thuộc tính xác minh như số nhân viên hoặc số an sinh xã hội.

Những kỹ thuật được đề cặp ở đây là không chính xác và do đó có thể chỉ sử dụng để boostrap quá trình trình ánh xạ lược đồ. Bất kỳ ánh xạ nào cũng phải được xác minh và xác nhận bởi những người chuyên gia.

## 3\. Ghi liên kết - Record Linkage

Chúng ta sẽ bắt đầu thảo luận về vấn đề mẫu ghi liên kết bằng một ví dụ cụ thể. Sau đó, chúng ta sẽ đưa ra một cái nhìn tổng quan về một phương pháp tiếp cận điển hình để giải quyết vấn đề này.

### 3.1 Vấn đề mẫu ghi liên kết - A Sample Record Linkage Problem

Giả sử rằng chúng ta có dữ liệu với hai bảng. Vấn đề mẫu ghi liên kết liên quan tới việc dự đoán mẫu ghi $a\_1$ giống với mẫu ghi $b\_1$ và mẫu ghi $a\_3$ giống với mẫu ghi $b\_2$. Giống như việc ánh xạ lược đồ, đây là những dự đoán không chính xác và cần phải được xác nhận bởi con người.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image5.png)

Một đồ thị tri thức lớn có thể chứa lượng thông tin trên 10 triệu công ty. Nó có thể nhận một nguồn cung cấp dữ liệu, mà được rút trích từ văn bản ngôn ngữ tự nhiên. Những nguồn cung cấp dữ liệu như thế có thể chứa hơn 100,000 công tin. Cho dù nếu một đồ thị tri thức có một phương thức chuẩn hoá để tham chiếu đến những công tin, nhưng nguồn dữ liệu mới được rút trích từ văn bản sẽ không có những bộ định danh chuẩn hoá. Tác vụ mẫu ghi liên kết là liên hệ những công ty mà chứa những nguồn cung cấp mới với những công ty đã tồn tại trong đồ thị tri thức. Vì các khối dữ liệu rất lớn, thực hiện tác vụ này một cách hiểu quả là điều tối quan trọng.

### 3.2 Phương pháp tiếp cận giải quyết vấn đề mẫu ghi liên kết

Độ hiệu quả của mẫu ghi liên kết (record linkage) liên quan tới hai bước: blocking và matching. Bước blocking liên quan tới một tính toán nhanh để chọn ra một tập con những mẫu ghi từ nguồn và mục tiêu mà sẽ được xem trong suốt một bước đối sánh chính xác và tốn kém hơn. Trong bước matching, chúng tôi đối sánh theo từng cặp với tập hợp con các bản ghi đã được chọn trong quá trình blocking. Trong ví dụ được đề cập ở trên, chúng ta có thể sử dụng một chiến lược blocking xem xét đối sánh chỉ những mẫu ghi mà phù hợp với trạng thái. Với chiến lược đó, chúng ta chỉ cần phải xem xét sự phù hợp $a\_1$ với $b\_1$, $a\_3$ với $b\_2$ do đó giảm đáng kể số lần so sánh phải thực hiện.

Cả hai bước blocking và matching thực hiện bằng cách học một random forest thông qua một quá trình học chủ động (active learning process). Một random forest là một tập của các luật quyết định mà được cho bởi những dữ đoán cuối cùng thông qua đa số phiếu được bầu được trả về bởi những luật riêng lẻ. Active learning (Học chủ động) là một quá trình học mà được xây dựng random forest bằng cách chủ động theo dõi hiệu suất của nó trên tập dữ liệu kiểm tra và lựa chọn có chọn lọc những mẫu huấn luyện mới để cải thiện hiệu suất của nó. Chúng ta sẽ giải thích chi tiết hơn hai bước này ở phần kế tiếp.

### 3.3 Random Forests

Những luật blocking dựa trên hàm kiểm tra chuẩn hoá độ tương đồng, giống như, độ phụ hợp chính xác - exact match, tương đồng Jaccard - Jaccarc Similarity, tương đồng chồng chéo - overlap similarity, tương đồng cosin - cosine similarity, … Lấy ví dụ, nếu chúng ta đã kiểm tra tương đồng chồng chéo giữa “Prolific Consulting” và “Prolific Consulting Inc.”, đầu tiên chúng ta sẽ thu thập những token trong mỗi chúng, và sau đó kiểm tra những token nào là chung, cho chung ta một điểm tương đồng là 2/3

Chúng ta biểu diễn một phần của một random forest cho blocking. Một random forest có thể được quan sát như một tập các luật. Random forest được hiển thị bên dưới là một tập của hai tập hợp luật. Các đối số của mỗi vị từ là hai giá trị được so sánh.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image6.png)

Có nhiều nguyên lý tổng quát cho việc tự động hoá việc chọn hàm tương đồng (similarity functions) cho luật blocking. Ví dụ, với những thuộc tính mang giá trị số học như tuổi – age, trọng lượng – weight, giá cả – price, … những hàm tương đồng ứng viên có thể là: khớp chính xác - exact match, hiệu tuyệt đối - absolute difference, hiệu tương đối - relative difference, và khoảng cách Levenstein - Levenstein distance. Với những thuộc tính mang giá trị chuỗi (string), người ta thường dùng edit distance, cosine similarity, Jaccard similarity, và TF/IDF functions.

### 3.4 Active Learning of Random Forests

Chúng ta có thể áp dụng Random Forest cho những luật blocking thông qua theo đổi quá trình học chủ động (active learning process). Chúng ta chọn một cách ngẫu nhiên một tập những cặp từ hai bộ dữ liệu. Bằng cách áp dụng hàm tương đồng lên mỗi thành phần của cặp, chúng ta có được một tập những đặc trưng cho mỗi cặp đó. Sử dụng những đặc trưng này, chúng ta sử dụng một Random Forest. Chúng ta áp dụng những luật có được lên một cặp mới được chọn từ tập dữ liệu, và đánh giá hiệu suất của chúng. Nếu hiệu suất dưới một ngưỡng (threshold) nhất định, chúng ta lặp lại chu trình, bằng cách cung cấp bổ sung những mẫu có nhãn cho đến khi hiệu suất chấp nhận được được tìm thấy. Chúng ta sẽ minh hoạ quá trình này bằng ví dụ ngay sau đây.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-26-how-to-create-a-knowledge-graph-from-data/media/image7.png)

Chúng ta giả định rằng bộ dữ liệu đầu tiên chứa ba thành phần: $a$, $b$, và $c$ và bộ dữ liệu thứ hai chứa hai thành phần $d$ và $e$. Từ bộ dữ liệu này, chúng ta lấy hai cặp $(a, d)$ và $(c, d)$ được gán nhãn tương đồng và không tương đồng bởi người dùng. Trên cặp này, chúng ta áp dụng những hàm tương đồng mà mỗi hàm sẽ cho ra kết quả là một đặc trưng của cặp. Sau đó chúng ta sử dụng những đặc trưng này để học một random forest. Chúng ta áp dụng những luật đã được học cho những bộ ba không nằm trong tập huấn luyện và hỏi người dùng để xác minh kết quả. Người dùng thông báo cho chúng ta biết là cặp $(b, d)$ là không đúng. Chúng ta thêm $(b, d)$ vào tập dữ liệu huấn luyện của chúng ta, và chúng ta lặp lại quá trình với vòng lặp tiếp theo. Sau một số vòng lặp, chúng ta dự đoán xem quá trình hội tụ chưa và cho chúng ta một Random forest để chúng ta có thể sử dụng một cách hiệu quản trong bước blocking.

Khi một Random forest đã được học, chúng ta có thể biểu diễn mỗi một luật cho người dùng. Dựa trên xác minh của người dùng, chúng ta chọn ra những luật sẽ được sử dụng trong những bước tiếp theo.

### 3.5 Applying the Rules

Sau khi chúng ta học được những luật, bước kế tiếp là áp dụng chúng lên dữ liệu thật sự. Khi kích thước dữ liệu là cực lớn, nó vẫn không thể áp dụng những luật blocking cho tất cả các cặp đối tượng. Do đó, chúng ta phải dùng đến lập chỉ mục (resort to indexing). Giả sử sằng, một trong các luật yêu cầu chỉ mục Jaccard nên phải lớn hơn $0.7$, và chúng ta đang tìm kiếm phù hợp với bộ phim Sound of Music. Vì độ dài của tên bộ phim là $3$, chúng ta chỉ cần phải xem xét những bộ phim trong dữ liệu của chúng ta mà độ dài của chúng nằm giữa $3 \\times 0.7$ và $3/0.7$, tức là nằm giữa 2 và 4. Nếu chúng ta đã lập chỉ mục tập dữ liệu về kích thước của phim, nó rất hiệu quả để chọn được những bộ phim mà kích thước tên nằm giữa $2$ và $4$, và lọc tập hơn thông qua việc áp dụng những luật blocking.

### 3.6 Performing the Matching

Bước blocking tạo ra một tạp những tập được tinh giảm đi rất nhiều mà đã được kiểm tra xem chúng có khớp với nhau hay không. Cấu trúc chung cho quá trình matching khá là tương tự với lần đầu chúng ta xác định một tập những đặc trưng, học một random forest, và thông qua quá trình active learning mà tinh chỉnh nó. Điểm khác biệt mấu chốt giữa bước blocking và matching là quá trình matching cần phải chính xác và cần nhiều tính toán. Bởi vì đây là bước cuối cùng trong mẫu ghi liên kết (record linkage) và chúng ta cần có độ tin cậy cao rằng hai thực thể phải chắc chắn khớp với nhau.

## 4\. Tổng kết

Trong chương này, chúng ta đề cập đến vấn đề khởi tạo một đồ thị tri thức bằng cách tích hợp dữ liệu đến từ những nguồn có cấu trúc. Lược đồ tích hợp của đồ thị tri thức có thể được tinh chỉnh và đánh giá theo mỗi yêu cầu của doanh nghiệp. Việc ánh xạ giữa những lược đồ của những nguồn khác nhau có thể được boostrapped thông qua những kỹ thuật thuật tự động, những chúng cần có xác mình đầu vào của con người. Record linkage - mẫu ghi liên kết là sự tích hợp dự liệu ở mức thể hiện, nơi mà chúng ta cần phải dự đoán đối sánh giữa hai thể hiện trong trường hợp không có bộ định danh duy nhất. Phương pháp tiếp cận chung nhất cho record linkage là học một Random Forest thông qua quá trình active learning. Với những ứng dụng yêu cầu độ chính xác cao, tính toán record linkage một cách tự động vẫn cần đến sự xác minh của con người.

Bài tập:

…Sẽ cập nhật sau…

Bài giảng gốc: [https://web.stanford.edu/class/cs520/2020/notes/How\_To\_Create\_A\_Knowledge\_Graph\_From\_Data.html]()
