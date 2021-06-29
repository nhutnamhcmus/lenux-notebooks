---
layout: post
toc: true
comments: true
---
**ĐỒ THỊ TRI THỨC - KNOWLEDGE GRAPH**

Đây là bản dịch từ Course CS520: Knowledge Graphs | Data Models, Knowledge Acquisition, Inference and Applications

Department of Computer Science, Stanford University, Spring 2021

Knowledge graphs have emerged as a compelling abstraction for organizing world's structured knowledge over the internet, capturing relationships among key entities of interest to enterprises, and a way to integrate information extracted from multiple data sources. Knowledge graphs have also started to play a central role in machine learning and natural language processing as a method to incorporate world knowledge, as a target knowledge representation for extracted knowledge, and for explaining what is being learned. This class is a graduate level research seminar and will include lectures on knowledge graph topics (e.g., data models, creation, inference, access) and invited lectures from prominent researchers and industry practitioners. The seminar emphasizes synthesis of AI, database systems and HCI in creating integrated intelligent systems centered around knowledge graphs.

Mục đích: Là tìm hiểu cũng như trau dồi kiến thức chuyên môn trong lĩnh vực Knowledge Graph cũng như từ vựng tiếng Anh. Không vì mục đích kinh doanh hay bất cứ mục đích về lợi nhuận, tất cả là vì mục đích chia sẻ kiến thức và học tập.

Mọi thông tin về những chủ đề được note lại có thể tìm thấy ở đây:

https://web.stanford.edu/class/cs520/2020/notes/Table\_Of\_Contents.html

Video của các buổi seminar trên địa chỉ Youtube:

https://www.youtube.com/playlist?list=PLDhh0lALedc5paY4N3NRZ3j\_ui9foL7Qc

Mọi vấn đề về dịch thuật, thuật ngữ xin để lại comment hoặc gửi về địa chỉ email: lenam.fithcmus@gmail.com với tiêu đề

\[ISSUES OF KG TRANSLATION\]

# WHAT ARE SOME HIGH VALUE CASES OF KNOWLEDGE GRAPHS?

MỘT SỐ TRƯỜNG HỢP GIÁ TRỊ CAO CỦA ĐỒ THỊ TRI THỨC

## 1\. Giới thiệu

Đồ thị tri thức được sử dụng trong một phạm vi ứng dụng rộng từ không gian (space), ngành báo chí (journalism), y sinh học (biomedicine) cho đến lĩnh vực giải trí (entertainment), bảo mật không gian mạng (network security) và dược phẩm (pharmaceuticals). Chúng ta không thể nào thảo luận một cách đầy đủ về những ứng dụng của đồ thị tri thức trong một chương ngắn như thế này. Do đó, chúng ta chọn ngành công nghiệp tài chính để mà mô tả ba trường hợp ứng dụng khác nhau của đồ thị tri thức: analytics - phân tích, tax calculations - tính toán thuế và báo cáo tài chính - financial reporting. Việc sử dụng đồ thị tri thức cho phân tích có lẽ là cách sử dụng phổ biến nhất. Việc sử dụng đồ thị tri thức trong tính toán thuế (hoặc, một cách tổng quát hơn, cho tính toàn tài chính) khá là tương tự như cách sử dụng chúng trong các chương trình dịch (compilers) và ngôn ngữ lập trình (programming languages). Sử dụng đồ thị tri thức trong trao đổi dữ liệu báo cáo là một lĩnh vực mới nổi của ứng dụng đồ thị tri thức mà sẽ còn tiếp tục trở nên quan trọng hơn trong tương lai sắp tới.

## 2\. Đồ thị tri thức trong phân tích tài chính - Knowledge Graphs for Financial Analytics

Xem xét một tổ chức tài chính lớn như một ngân hàng phải giải quyết với hàng triệu khách hàng mà một vài trong số đó là những công ty, và một vài trong số đó là những cá nhân. Những tổ chức như thế thường xuyên đối mặt với những câu hỏi có thể tạo ra theo những mẫu dưới đây:

1\. Nếu rằng một công ty đi vào tình trạng khó khăn tài chính, liệu những khác hàng của chúng ta là những nhà cung cấp và những nhà phân phối nào?

2\. Trong một mạng lưới chuỗi cung ứng, liệu có một công ty đơn lẻ nào đó liên kết với một nhóm các công ty?

3\. Những công ty khởi nghiệp nào đã thu hút được các nhà đầu tư có ảnh hưởng nhất?

4\. Nhóm những nhà đầu tư nào có xung hướng đầu tư cổ phần?

5\. Những công ty nào là giống với một công ty cho trước nhất?

**6. Công ty nào có thể là một khách hàng tốt trong tương lai cho chúng ta?**

Để trả lời câu hỏi thứ nhất bên trên, chúng ta cần dữ liệu về những nhà cung cấp và phân phố của một công ty. Những dữ liệu như vậy thường sẵn có thông qua những nhà cung cấp dữ liệu thứ ba và phải được trả phí. Những dữ liệu bên ngoài về những nhà cung cấp và phân phố phải được kết hợp với dữ liệu bên trong một công ty. Tận dụng những kỹ thuật của ánh xạ lược đồ (schema mapping) và liên kết thực thể (entity linking) mà chúng ta đã đề cập trong chương 4 cho việc khởi tạo một đồ thị tri thức từ dữ liệu có cấu trúc. Càng ngày, các tổ chức càng bắt đầu tận dụng dữ liệu từ tin tức hàng ngày để cung cấp thông tin thị trường. Để tận dụng những tin tức tài chính, chúng ta sẽ cần phải rút trích thông tin từ văn bản sử dụng các kỹ thuật rút trích thực thể (entity extraction) và rút trích quan hệ (relation extraction) mà đã được mô tả trong chương 5. Khi một đồ thi tri thức được hoàn thiện, chúng ta có thể sử dụng những thuật toán tìm kiếm đường đi mà đã được đề cập trong chương 6 để trả lời những truy vấn. Giả sử đồ thị tri thức của chúng ta biểu biễn mỗi quan hệ nhà phân phối và nhà cung ứng giữa các công ty, các những thuật toán duyệt cần phải duyệt qua những mối quan hệ để trả lời những truy vấn. Các kết quả truy vấn có thể hữu ích nếu chúng ta sử dụng một trực quan hoá đơn giản của chuỗi cung ứng. Để trả lời câu hỏi thứ hai, chúng ta có thể tận dụng những kỹ thuật xác định trung tâm. Đặc biệt là, betweenness centrality là một phương pháp tiếp cận có thể dùng cho việc xác định công ty nào đóng vai trò trung tâm trong chuỗi cung ứng.

Câu hỏi thứ ba bên trên có liên quan rõ ràng đến việc định giá một công ty khởi nghiệp. Giống như trong câu hỏi đầu tiên, câu trả lời yêu cầu những dữ liệu ban đầu về các khoản đầu tư từ một nhà cung cấp bên thứ ba, và tích hợp nó với dữ liệu khách hàng nội bộ. Việc trả lời câu truy vấn yêu cầu sử dụng những kỹ thuật xác định trung tâm mà chúng ta đã đề cập qua trong chương 6. Đặc biệt là, thuật toán PageRank là một kỹ thuật thích hợp cho việc trả lời câu hỏi vì thích ứng tốt với đồ thị. Biểu diễn câu trả lời sẽ có lợi ích bằng cách trình bày một trực quan đồ hoạ về cách các nhà đầu tư có ảnh hưởng được kết nối với các công ty khởi nghiệp khác nhau mà họ tham gia. Câu hỏi thứ tư là một ví dụ về xác định cộng đồng. Trong một đồ thị tri thức để nắm bắt những quan hệ các khoản đầu tư, những nhà đầu tư, những người mà cùng đầu tư vào một công ty sẽ tạo ra một dạng cộng đồng.  
Câu hỏi thứ năm và thứ sáu là những ví dụ về những kỹ thuật suy luận dựa trên Graph Embeddings mà đã được giới thiệu sơ qua trong chương 1. Câu hỏi thứ năm có thể được trả lời bằng những kỹ thuật về tính toán độ tương đồng dựa trên các embedding vector cho những nút được quan tâm. Câu hỏi thứ sau có thể là một thể hiện của vấn đề **link prediction** trong một đồ thị mà khá là tương tự với vấn đề giải quyết trong một mô hình ngôn ngữ. Ở đây, thay vì dự đoán từ kế tiếp là gì, chúng ta quan tâm đến việc dự đoán những liên kết có khả năng xảy ra nhất từ một nút cho trước.

## 3\. Đồ thị tri thức trong tính toán thuế thu nhập - Knowledge Graphs for Income Tax Calculations

Luật thuế thu nhập ở Hoa Kỳ bao gồm hơn 80,000 trang văn bản. Mỗi năm, có hơn 150 triệu thuế thu nhập được nộp. Luật thuế thu nhập của Hoa Kỳ bao gồm hàng ngàn mẫu và hướng dẫn mà có thể xuất hiện trong bất kỳ một thu nhập nào. Những yêu cầu thay đổi hằng năm, và đôi khi có thể thay trong giữa năm của một năm khai thuế. Với sự ra đời của phần mềm khai thuế thu nhập, những luật khó hiệu này có thể khả năng truy cập cho những người dùng để mà họ có thể chuẩn bị và tự mình nộp thuế thu nhập.

Một vài công cụ chuẩn bị cho thuế thu nhập biểu diễn những luật thuế bằng cách sử dụng một tập các luật. Khi những luật này được biểu diễn bởi những luật logic, nó không thể được sử dụng cho tính toán, mà cũng không thể cho việc sinh ra những hộp thoại người dùng (user dialogs), cung cấp những giải thích, kiểm tra tính hoàn thiện của đầu vào, … Trong khi tính toán thuế thu nhập cần những luật suy luận tương tự như những gì chúng ta đã đề cập trong chương 6, nhưng những thao tác hỗ trợ như sinh ra hộp thoại người dùng, quyết định tác động của việc thay đổi một luật cho toàn bộ phần còn lại của hệ thống, được hoàn thành bởi mô hình hoá những luật như một đồ thị, và sử dụng những thuật toán dựa trên đồ thị để thực hiện những tính toán đó. Để cụ thể cách sử dụng đồ thị tri thức, xem xét một luật dưới đây từ luật thuế thu nhập:

Một người đủ điều kiện để hưởng lợi ích về thuế nếu:

\- người đó là một cư dân của California và

\- tuổi của người đó phải từ 18 tuổi trở lên

Chúng ta có thể biểu diễn cái luật này như một luật Datalog như sau:

qualified\_for\_tax\_benefit(P) :-

resident\_of(P,CA) & age(P,N) & min(N,18,18)

Với luật trên, chúng ta có thể xây dựng một đồ thị tri thức như sau

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-29-what-are-some-high-value-use-cases-of-knowledge-graphs/media/image1.png)Nếu chúng tôi đang chuẩn bị tờ khai thuế cho một người 17 tuổi, thông qua phân tích khả năng tiếp cận trên biểu đồ trên, chúng ta có thể xác định rằng trong mọi trường hợp, người đó sẽ không đủ tiêu chuẩn, và do đó không cần thiết phải xác định nơi cư trú của họ. Ví dụ bên trên là nhỏ vì nó đánh giá chỉ một luật. Tuy nhiên, như đã nói trước đó, hàng nghìn quy tắc có thể áp dụng cho một người và trong thực tế, phân tích như vậy cần được thực hiện trên một đồ thị rất lớn và phức tạp.

## 4\. Đồ thị tri thức trong báo cáo tài chính - Knowledge Graphs for Financial Reporting

Các tổ chức tài chính được yêu cầu báo cáo các hợp đồng phái sinh mà họ hiện đang nắm giữ. Những ví dụ về những hợp đồng như thế bao gồm hoán đổi lãi suất và hàng hóa, quyền chọn, hợp đồng tương lai và kỳ hạn, và các chứng khoán khác nhau được bảo đảm bằng tài sản. Các báo cáo như vậy rất được quan tâm của các nhóm tiếp nhận phản ánh trong một tổ chức, các nhà môi giới và đại lý, những người cần hiểu và quản lý các danh mục đầu tư đó cũng như các cơ quan quản lý cần phân tích và giám sát các thị trường này. Nếu mỗi tổ chức tài chính cung cấp những báo cáo này trong một hình thức khác, nó trở thành thách thức với các bên liên quan trong việc xử lý, tổng hợp và hiểu ý nghĩa của những báo cáo này. Đó là một vấn đề thể hiện kinh điển trong vấn đề tích hợp dữ liệu mà đồ thị tri thức phải giải quyết.

Một sáng kiến trong toàn ngành để giải quyết vấn đề như vậy là dựa trên phương pháp tiếp cận định nghĩa một mô hình ngữ nghĩa chung, gọi là Financial Industry Business Ontology (FIBO). FIBO được định nghĩa bằng cách sử dụng một ngôn ngữ hình thức gọi là Web Ontology Language (OWL). FIBO xác định những thứ mà được quan tâm trong những ứng dụng kinh doanh tài chính và cách mà những thứ đó liên hệ với nhau. Theo cách này, FIBO có thể cung cấp ý nghĩa cho bất kỳ dữ liệu nào (ví dụ như, spreadsheets, relational databases, XML documents) mà mô tả hoạt động kinh doanh tài chính. Những khái niệm của FIBO được phát triển bởi một cộng đồng người dùng đến từ rất nhiều tổ chức tài chính và biểu diễn thống nhất những khái niệm chung được hiểu trong ngành và được phản ánh trong những mô hình dữ liệu ngành và các thông điệp chuẩn hoá.

FIBO cung cấp những khái niệm và thuật ngữ cần thiết cho các báo cáo chứng khoán phái sinh. Để giúp cho những người dùng mới bắt đầu với FIBO, những nhà phát triển cung cấp những mẫu để có thể bắt đầu mô hình hoá những khái niệm cơ sở như một Company, mã định danh pháp lý toàn cầu của nó, các công cụ phái sinh, … Ví dụ, FIBO định nghĩa rằng một Derivatives Contract (Hợp đồng phái sinh) có thể có một phần (has part) hoặc nhiều tuỳ chọn (Options). Một tuỳ chọn (option) có thể gọi là một call option buyer. Dưới đây là một biểu diễn đồ hoạ của các liên kết từ một call option buyer đến những thực thể liên hệ:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-29-what-are-some-high-value-use-cases-of-knowledge-graphs/media/image2.png)

Đồ thị phía trên là một đồ thị ontology có nghĩa là nó không nắm bắt mối quan hệ giữa các giá trị dữ liệu mà là các mối quan hệ tồn tại ở cấp độ lược đồ. Ví dụ, ta nhận thấy rằng một call option buyer phải là một bên độc lập, một pháp nhân và một đại lý tự quản. Khi một tổ chức tài chính sử dụng những thuật ngữ và định nghĩa từ FIBO cho báo báo tài chính mà nó phát sinh, nó cung cấp khởi tạo đầu cho báo cáo tích hợp của nó đến từ những nhà cung cấp khác. Sử dụng FIBO có thể tinh giản và giảm thiểu chi phí đáng kể trong tổng hợp và hiểu thông tin từ những hợp đồng phái sinh.

Sự phát triển của FIBO được thúc đẩy bởi một tập hợp các trường hợp sử dụng thúc đẩy. Hợp đồng phái sinh chỉ là một trong nhiều các trường hợp chưa được đề cập. Các trường hợp khác bao gồm tiếp xúc đối tác, phân tích chỉ số để phát triển ETF và cung cấp dữ liệu công cụ trao đổi.

## 5\. Tổng kết

Đồ thị tri thức có phạm vi ứng dụng rộng trên nhiều ngành. Trong chương này, chúng ta chọn tập trong vào ba sử dụng khác nhau của đồ thị tri thức trong ngành tài chính: phân tích – analytics, tính toán - calculations và báo cáo (reporting). Sử dụng đồ thị tri thức cho phân tích là cách sử dụng phổ biến và chủ đạo nhất vì nó có khả năng cung cấp những hiểu biết hữu về dữ liệu mà một tổ chức sở hữu. Sử dụng đồ thị tri thức cho tính toán đã tồn tại khá lâu vì nó tương tự như sử dụng đồ thị trong chương trình dịch (compilers) và các rule engine cho nhiều tác vụ phân tích và suy luận. Cuối cùng, sử dụng Ontology trong trao đổi dữ liệu là một lĩnh vực mới nổi cho đồ thi tri thức với tìm năng to lớn, sẽ ngày càng quan trọng và đóng vai trò chủ đạo trong tương lai.

**Bài tập:**

...Sẽ cập nhật sau…

Bài giảng gốc: https://web.stanford.edu/class/cs520/2020/notes/What\_Are\_Some\_High\_Value\_Use\_Cases\_Of\_Knowledge\_Graphs.html
