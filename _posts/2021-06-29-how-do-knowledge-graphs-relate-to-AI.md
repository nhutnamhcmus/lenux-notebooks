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

# HOW DO KNOWLEDGE GRAPHS RELATE TO AI?

ĐỒ THỊ TRI THỨC LIÊN HỆ NHƯ THẾ NÀO ĐẾN TRÍ TUỆ NHÂN TẠO

## 1\. Giới thiệu

Trong chương cuối cùng này, chúng ta sẽ thảo luận những con đường khác nhau mà đồ thị tri thức (knowledge graphs) giao nhau với Trí tuệ Nhân tạo (Artificial Intelligence). Như chúng ta cũng có nói đến trong chương mở đầu, việc sử dụng một đồ thị hữu hướng được gán nhãn (labeled directed graphs) cho biểu diễn tri thức (knowledge representation) đã hiện diện từ những ngày đầu của Trí tuệ Nhân tạo (AI). Sự tập trung của chúng ta trong phần thảo luận của chương này là trong việc sử dụng đồ thị tri thức trong những phát triển gần đây. Do đó, chúng ta chọn ba chủ đề để nói thêm: knowledge graphs as a test bed for AI algorithms - đồ thị tri thức như một môi trường kiểm thử cho các thuật toán AI, emerging new specialty area of graph data science - lĩnh vực chuyên môn mới nổi của khoa học dữ liệu đồ thị, và knowledge graphs in the broader context of achieving the ultimate vision of AI - đồ thị tri thức trong một ngữ cảnh rộng lớn hơn để đạt dược tầm nhìn cuối cùng của AI.

## 2\. Đồ thị tri thức như một nơi thử nghiệm cho các thuật toán AI thế hệ hiện tại - Knowledge Graphs as a Test-Bed for Current Generation AI Algorithms

Đồ thị tri thức có hai cách liên hệ với những thuật toán AI. Một là, đồ thị tri thức kích hoạt rất nhiều ứng dụng AI hiện tại, và hai là, rất nhiều thuật toán AI hiện tại được sử dụng trong khởi tạo đồ thị tri thức. Chúng ta sẽ đề cập sức mạnh tổ hợp cộng sinh (symbiotic synergy) này trong cả hai hướng.

Trợ lý cá nhân (personal assistants), những hệ thống gợi ý (recommender systems) và các search engine là những ứng dụng thể hiện những hành vi thông minh và có hàng tỉ người dùng. Người ta hiện nay đã chấp nhận rằng những ứng dụng này sẽ hoạt động tốt hơn nếu chúng có thể tận dụng được đồ thị tri thức. Một trợ lý cá nhân (personal assistants) sử dụng một đồ thị tri thức để có thể hoàn thành nhiều công việc hơn. Một hệ thống gợi ý (recommender systems) với một đồ thị tri thức có thể tạo ra những gợi ý tốt hơn. Và tương tự, một search engine có thể trả ra những kết quả tốt hơn khi nó truy cập đến một đồ thị tri thức. Bởi vậy, những ứng dụng này cung cấp một ngữ cảnh đầy hấp dẫn và một tập những yêu cầu cho đồ thị tri thức để có những tác động đến việc cung cấp những sản phẩm ngay tức thì.

Để khởi tạo một đồ thị tri thức, chúng ta phải tiếp thu tri thức từ nhiều nguồn thông tin, sắp xếp những thông tin đó, chắt lọc những thông tin quan trọng (distill key pieces) từ biển thông tin to lớn đó và khai thác tri thức để rút trích sự khôn ngoan (wisdom) mà có thể tác động đến những hành vi thông minh. Những kỹ thuật Trí tuệ Nhân tạo đóng vai trò trọng tâm trong từng bước khởi tạo đồ thị tri thức và khai phá đồ thị tri thức. Với việc rút trích thông tin thông qua nhiều nguồn dữ liệu, chúng ta sử dụng những kỹ thuật như ánh xạ lược đồ (schema mapping) và liên kết thực thể (entity linking). Để chắt lọc thông tin, chúng ta có thể sử dụng những kỹ thuật như data cleaning (làm sạch dữ liệu) và anomaly detection (phát hiện bất thường). Và cuối cùng, để rút trích sự ngôn ngoan (wisdom) từ đồ thị chúng ta sử dụng những thuật toán suy luận (inference algorithms), trả lời câu hỏi ngôn ngữ tự nhiên (natural language question answering). ….

Vì thế, đồ thị tri thức kích hoạt những hệ thống AI (AI systems), cung cấp những động lực và một tập những yêu cầu cho chúng. Những kỹ thuật Trí tuệ Nhân tạo cũng thúc đẩy khả năng của chúng ta trong việc khởi tạo đồ thị tri thức một cách thương mai hoá và mở rộng phạm vi.

## 3\. Đồ thị tri thức và Khoa học dữ liệu đồ thị - Knowledge Graphs and Graph Data Science

Khoa học Dữ liệu Đồ thị (Graph Data Science) là một ngành mới nổi lên nhằm mục đích thu thập tri thức bằng cách tận dụng cấu trúc trong dữ liệu. Thông thường những tổ chức truy cập đến một lượng dữ liệu khổng lồ, những khả năng của họ để tận dụng lượng dữ liệu này bị hạn chế bởi một tập hợp các báo cáo đặt trước được tạo bằng cách sử dụng dữ liệu đó. Phạm vi của Khoa học Dữ liệu Đồ thị (Graph Data Science) đang biến đổi cách làm đó bằng cách kết hợp những thuật toán đồ thị (Graph Algorithms), truy vấn đồ thị (Graph Queries) và trực quan hoá (Visualization) thành những sản phẩm mà tăng tốc xử lý thu thập thông tin hữu ích một cách đáng kể.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-29-how-do-knowledge-graphs-relate-to-AI/media/image1.png)

Như chúng ta đã thấy trong định hướng phân tích (analytics-oriented) sử dụng các trường hợp cho tài chính công nghiệp (financial industry), kinh doanh (businesses) quan tâm đến khai phá cấu trúc quan hệ (relational structure) trong dữ liệu của họ để tạo ra những dự đoán về rủi ro, những thị trường cơ hội mới, … Trong việc tạo ra những dự đoán, người ta sử dụng phổ biến những thuật toán máy học (machine learning algorithms) mà dựa trên những kỹ thuật đặc trưng (feature engineering) một cách cẩn thận. Vì những thuật toán máy học bây giờ trở thành như một món hàng và có thể được sử dụng như những sản phẩm bán sẵn, do đó nổi nên một kỹ năng khác biệt của kỹ thuật đặc trưng (feature engineering). Kỹ thuật đặc trưng (feature engineering) yêu cầu một sự hiểu biết sâu về một lĩnh vực như hiểu về nguyên lý hoạt động của các thuật toán máy học.

Chính sức mạnh tổng hợp giữa hệ thống dựa trên đồ thị truyền thống và những mô hình máy học sẵn có để xác định và dự đoán những thuộc tính trong dự liệu, điều đó đã xúc tác tạo ra một ngành con của Khoa học Dữ liệu Đồ thị (Graph Data Science) . Do các trường hợp sử dụng có tác động cao có thể thông qua khoa học dữ liệu đồ thị, nó trở thành một kỹ năng mềm được săn đón trong ngành công nghiệp hiện nay.

## 4\. Đồ thị tri thức và mục tiêu dài hạn của AI - Knowledge Graphs and Longer-Term Objectives of AI

Những công trình đầu tiên trong AI tập trung vào tận dụng biểu diễn tri thức và khởi tạo lĩnh vực đồ thị tri thức thông qua biểu diễn như semantic networks (mạng ngữ nghĩa). Khi lĩnh vực này phát triển, semantic networks (mạng ngữ nghĩa) được chính thức hoá và dẫn đến nhiều thế hệ các ngôn ngữ biểu diễn như description logics - biểu diễn logic, logic programs - chương trình lgoic, và graphical models - mô hình đồ hoạ. Theo suốt quá trình phát triển của những ngôn ngữ này, một thách thức quan trọng không kém của việc tạo ra tri thức trong chủ nghĩa hình thức đã chọn đã được giải quyết. Những kỹ thuật cho việc tạo ra tri thức bắt đầu từ knowledge engineering - kỹ thuật tri thức, inductive learning - học quy nạp, và gần đây hơn là deep learning methods - những phương thức học sâu.

Để hiện thực hóa tầm nhìn của AI, biểu diễn tri thức một cách rõ ràng về một miền phù hợp với sự hiểu biết của con người và cho phép lập luận với miền đó là điều cần thiết. Trong khi thực hiện một số tác vụ, như search - tìm kiếm, recommendation - gợi ý, translation – dịch, … human understanding - sự hiểu biết của con người và precision không yêu cầu quá khó khăn, nhưng trong đa số miền thì những yêu cầu này là cần thiết. Ví dụ về nhưng miền như vậy bao gồm tri thức về luật pháp để tính toán thuế, tri thức về một môn học cho việc giảng dạy nó cho sinh viên, kiến thức về hợp đồng để mà một máy tính có thể thực thi nó một cách tự động, … Hơn nữa, ngày càng được công nhận rằng trong nhiều tình huống mà chúng ta có thể đạt được hành vi thông minh mà không cần trình biểu diễn tri thức rõ ràng, thì hành vị vẫn cần phải được giải thích để con người có thể hiểu lý do của nó. Với lý do này, chúng ta tin rằng, biểu diễn rõ ràng là cần thiết.

Có câu chuyện trong cộng đồng nghiên cứu rằng kỹ thuật tri thức không mở rộng quy mô, và Xử lý ngôn ngữ tự nhiên và những phương thức máy học sẽ mở rộng được quy mô. Những phát biểu như vậy dựa trên sự mô tả không chính xác các nhiệm vụ được giải quyết bằng xử lý ngôn ngữ tự nhiên. Ví dụ, sử dụng một mô hình ngôn ngữ, chúng ta có thể tính toán từ tương đồng (word similarity), nhưng mô hình ngôn ngữ không cho chúng ta thông tin về lý do cho sự tương đồng đó . Ngược lại, khi chúng ta sử dụng một nguồn tài nguyên như Wordnet với việc tính toán từ tương đồng (word similarity), chúng ta biết chính xác cơ sở cho sự tương đồng đó. Một mô hình ngôn ngữ có thể đạt được quy mô, nhưng cái giá là sự hiểu biết của con người về những kết luận của nó. Thành công của phương thức web-scale phụ thuộc cốt yếu vào đầu vào của con người dưới dạng hyperlink, click data hoặc phản hồi rõ ràng của người dùng. Tận dụng những phương thức có thể mở rộng và tự động hóa dê tạo ra những đồ thị tri thức mà con người có thể hiểu được và sử dụng chúng để đạt được những hành vi thông minh đúng dắn để giải quyết cho một hệ thống AI nên thực hiện như thế nào.

Chúng ta đều biết rằng một biểu diễn đồ thị có nhãn đơn giản ( a simple labeled graph representation) thì không đủ cho nhiều mong muốn hiệu suất những tác vụ từ AI. Đó chính xác là lý do cho việc phát triển nhiều hơn những biểu diễn hình thức cảm xúc. Do nhu cầu giải quyết vấn đề trong kinh tế và quy mô khởi tạo của những biểu diễn, biểu cảm hình thức (expressive formalisms) rất ích khi được sử dụng phổ biến, nhưng nó không ngụ ý rằng các vấn đề mà các hình thức giải quyết như vậy đã được giải quyết bằng những phương pháp học sâu và NLP mới nhất. Một vài ví dụ cho vấn đề này như self-awareness - tự nhận thức, commonsense reasoning - suy luận chung chung, model-based reasoning - mô hình dựa trên suy luận, experimental design - thiết kế thực nghiệm, … Một hệ thống tự nhận thức (A self-aware system) có thể nhận biết và biểu diễn giới hạn về tri thức của riêng nó. Sự hiểu biết chung chung (Commonsense understanding) về thế giới cho một hệ thống khả năng nhận biết những tình huống rõ ràng là vô nghĩa, ví dụ như là một đồng xu có ghi ngày tháng năm 1800 trước Công nguyên, không thể là đồng xu thật. Những mô hình ngôn ngữ hiện tại có thể sinh ra những câu có nghĩa với độ dài nhất định, nhưng chúng thiếu một mô hình tường thuật tổng thể (an overall model of the narrative) để sinh ra những văn bản mạch lạc dài hơn. Tạo ra một chương trình AI có thể làm chủ một lĩnh vực, hình thành một giả thuyết, thiết kế thức nghiệm, và phân tích những kết quả của nó là một thách thức nằm ngoài tầm với của những hệ thống thế hệ hiện tại.

## 5\. Tổng kết

Chúng ta đề cập ba cách thức hoạt động khác nhau trên đồ thị tri thức giao nhau với AI: như một môi trường thử nghiệm cho việc đánh giá thuật toán máy học và NLP, như một bộ kích hoạt của một ngành mới nổi của Graph Data Science, và như một thành phần cốt lỗi trong việc hiện thực hoá mục tiêu dài hạn của AI. Chúng ta hy vọng rằng sau những chương này sẽ truyền cảm hứng cho nhiều người để tận dụng những gì có thể thông qua việc tạo ra các biểu đồ tri thức có thể mở rộng và khai thác chúng. Tuy nhiên chúng ta cũng không nên bỏ qua một tầm nhìn dài hạn hơn về việc tạo ra những biểu cảm và những biển diễn hiểu biết con người mà có thể được tạo ra trong một cách quy mô.

**Bài tập:**

...Sẽ cập nhật sau…

Bài giảng gốc: https://web.stanford.edu/class/cs520/2020/notes/How\_do\_Knowledge\_Graphs\_Relate\_To\_AI.html
