---
layout: post
---
**ĐỒ THỊ TRI THỨC - KNOWLEDGE GRAPH**

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

**WHAT IS A KNOWLEDGE GRAPH?**

**1. Giới thiệu**

Đồ thị tri thức là trừu tượng rất hợp lý cho việc tổ chức tri thức có cấu trúc của thế giới trên Internet, và như một cách tích hợp rút trích thông tin từ nhiều nguồn dữ liệu. Đồ thị tri thức cũng đóng vai trò trung tâm trong Machine Learning (Học Máy) như một phương pháp kết hợp tri thức nhân loại, như một mục tiêu biểu diễn tri thức (Knowledge Representation) với những tri thức đã được rút trích, và giải thích những gì học được.

Mục đích của chúng ta ở đây là để giải thích những thuật ngữ (terminology), khái niệm (concepts) và cách sử dụng của Đồ thị tri thức trong một cách hiểu đơn giản. Chúng ta không tổ chức một khảo sát toàn diện về những công trình quá khứ và hiện tại về đề tài Đồ thị tri thức.

Chúng ta sẽ bắt đầu bằng cách định nghĩa về đồ thị tri thức, một vài ứng dụng mà đóng góp vào sự phát triển phổ biến của Đồ thị tri thức, sau đó sử dụng Đồ thị tri thức vào trong Machine Learning (Học Máy). Chúng ta sẽ kết lại chương bằng một tổng kết chung về những điểm mới và khác biệt về phương pháp Đồ thị tri thức trong thời gian gần đây.

**2. Định nghĩa Đồ thị tri thức**

Một Đồ thị tri thức (Knowledge Graph) là một đồ thị hữu hướng được gán nhãn (Directed labeled graph – DLG) mà những nhãn này xác định có ý nghĩa rõ ràng.

Một đồ thị hữu hướng được gán nhãn (DLG) bao gồm các nút (nodes), cạnh liên kết (edges) và nhãn (labels). Bất kỳ thứ gì đều có thể xem là một nút (node), ví dụ như con người, công ty, máy tính, … . Một cạnh liên kết (edges) kết nối một cặp nút (nodes) và thể hiện mối quan hệ được quan giữa chúng, ví dụ như mối quan hệ tình bạn giữa hai người, mối quan hệ khách hàng giữa một công ty và một người, hoặc một kết nối mạng kết nối hai máy tính. Nhãn thể hiện ý nghĩa của mối quan hệ đó, ví dụ: mối quan hệ tình bạn giữa hai người.

Tổng quát hơn, cho một tập các nút N, và một tập các nhãn L, một đồ thị tri thức là một tập hợp con của tích hữu hướng N x L x N. Mỗi thành phần trong tập này được gọi là một bộ ba và có thể trực quan như sau:

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-25-what-is-knowled-graph/media/image1.png)

Biểu diễn đồ thị hữu hướng thường được sử dụng trong nhiều cách khác nhau phụ thuộc vào nhu cầu của ứng dụng. Một đồ thị hữu hướng như tập các node biểu diễn con người, và các cạnh liên kết thể hiện mối quan hệ tình bạn giữa họ còn được gọi là một dữ liệu đồ thị. Một đồ thị hữu hướng mà những node là những lớp đối tượng (sách, báo, …) và những cạnh liên kết thể hiện mối quan hệ lớp con có thể hiểu là một phân loại học (taxonomy). Trong một số mô hình dữ liệu, A được gọi là chủ thể (subject), B được gọi là thuộc tính (predicate), và C được gọi là đối tượng (object).

Nhiều tính toán dựa trên đồ thị có thể điều chỉnh thành dạng điều hướng. Ví dụ như, trong một đồ thị tri thưc tình bạn, để tính toán bạn bè của một người bạn của một người A, chúng ta có thể điều hướng đồ thị tri thức từ A đến tất cả các node B mà liên kết với nó bằng nhãn quan hệ bạn, và sau đó, đệ quy đến tất cả node C liên kết đến B bởi mối quan hệ bạn.

Một đường đi (Path) trong một đồ thị G là một chuỗi các node (v\_1, v\_2, …, v\_n) trong đó bất kỳ một node i nào thuộc N với 1 \\leq i \< n, tồn tại một cạnh liên kết từ v\_i đến v\_{i+1}.

Một đường đi đơn (SIMPle Path) là một đường đi mà không có node nào lặp lai

Một chu trình (Cycle) là một đường đi trong đó node bắt đầu và node kết thúc là giống nhau.

Thông thường thì, chúng ta quan tâm đến chỉ một vài đường đi mà nhãn cạnh liên kết giống với tất cả các cặp node. Có thể định nghĩa nhiều thuộc tính khác trên đồ thị (thành phần liên thông, thành phần liên thông mạnh) và những cách khác nhau để duyệt đồ thị như (đường đi ngắn nhất - shortest path, đường đi Hamiltonian, ….)

**3. Những ứng dụng gần đây của Đồ thị tri thức**

Có rất nhiều những ứng dụng của đồ thị tri thức cả trong nghiên cứu lẫn doanh nghiệp. Trong Khoa học máy tính, có rất nhều cách sử dụng biểu diễn đồ thị hữu hướng, ví dụ như, luồng dữ liệu đồ thị, sơ đồ quyết định nhị phân, biểu đồ trạng thái, … Ở đây chúng ta sẽ tập trung vào hai ứng ứng cụ thể dẫn đến sự phát triển phổ biến của đồ thị tri thức: tổ chức thông tin trên Internet, và tích hợp dữ liệu.

**3.1 Đồ thị tri thức trong việc tổ chức thông tin trên Internet**

Chúng ta sẽ giải thích việc sử dụng một đồ thị tri thức trên trang web bằng cách lấy ví dụ cụ thể về Wikidata. Wikidata đóng vai trò là nơi lưu trữ trung tâm cho dữ liệu có cấu trúc cho Wikipedia. Để cho thấy sự tác động lẫn nhau giữa hai đối tượng, và động lực của việc sử dụng đồ thị tri thức Wikidata, ta xem xét thành phố Winterthur ở Switzerland có một trang trên Wikipedia. Trang Wikipedia cho Winterthur liệt kê những thị trấn song sinh với nó: hai ở Switzerland, một ở Czech Republic, và một ở Austria. Thành phố của Ontario ở California có một trang Wikipedia với tựa đề dựa đặt là Ontario, California, liệt kê Winterhur như thành phố kết nghĩa của nó. Những quan hệ thành phố kết nghĩa và thành phố song sinh đồng nhất cũng như tương hỗ. Như vậy, nếu một thành phố A là một thành phố kết nghĩa của một thành phố khác B thì B phải là một thành phố kết nghĩa của A.Việc suy luận này nên tự động, nhưng vì thông tin này được nêu bằng tiếng Anh trong Wikipedia, nên không dễ phát hiện ra sự khác biệt này. Ngược lại, trong Wikidata, biểu diễn của Winterthur, có một mối quan hệ được gọi là cơ quan hành chính kết nghĩa liệt kê thành phố Ontario. Vì mối quan hệ này là đối xứng, trang Wikidata cho thành phố Ontario tự động bao gồm Winterthur. Do đó, khi đồ thị kiến thức Wikidata sẽ được tích hợp hoàn toàn vào Wikipedia, những sai lệch như vậy sẽ tự nhiên biến mất.

Wikidata bao gồm dữ liệu từ nhiều nhà cung cấp độc lập, ví dụ như Library of Congress, công bố dữ liệu chứa những thông tin về Winterthur. Bằng cách sử dụng bộ định danh (identifier) Wikidata cho Winterthur, thông tin được phát hành bởi Library of Congress có thể được liên kết một cách dễ dàng với những thông tin sẵn có từ những nguồn khác. Wikidata giúp dễ dàng thiết lập các liên kết như vậy bằng cách xuất bản các định nghĩa của các mối quan hệ được sử dụng trong nó trong Schema.Org.

Từ vựng quan hệ trong Schema.Org cho chúng ta, ít nhất, ba ưu điểm.

\- Thứ nhất, có thể viết các truy vấn trải dài trên nhiều tập dữ liệu

\- Thứ hai, với khả năng truy vấn như vậy, có thể dễ dàng tạo các khối thông tin có cấu trúc trong Wikipedia

\- Thứ ba, thông tin có cấu trúc được trả về bởi các truy vấn cũng có thể xuất hiện trong kết quả tìm kiếm, hiện là một tính năng tiêu chuẩn cho các công cụ tìm kiếm hàng đầu

Một phiên bản gần đây của Wikidata có hơn 80 triệu đối tượng, với hơn một tỷ quan hệ giữa những đối tượng này. Wikidata tạo ra những liên kết qua hơn 4872 danh mục khác nhau bằng 414 ngôn ngữ khác nhau do các nhà cung cấp dữ liệu độc lập xuất bản. Theo ước tính gần đây, 31% trang web và hơn 12 triệu nhà cung cấp dữ liệu xuất bản chú thích Schema.Org hiện đang sử dụng từ vựng của Schema.Org.

Một số đặc trưng chính của đồ thị tri thức Wikidata

\- Một đồ thị với quy mô chưa từng có, và là một đồ thị tri thức lớn nhất cho đến thời điểm hiện tại

\- Nó được tham gia xây dựng bởi một cộng đồng người đóng góp

\- Một số dữ liệu trong Wikidata có thể đến từ những thông tin được rút trích tự động, những nó phải dễ hiểu và được xác minh theo chính sách biên tập của Wikidata

\- Đó là một nỗ lực vô cùng để cung cấp các định nghĩa ngữ nghĩa của các tên quan hệ khác nhau thông qua từ vựng trong Schema.Org.

\- Mục tiêu chính của việc sử dụng Wikidata là cải thiện tìm kiếm trên web

Cho dù Wikidata có nhiều ứng dụng sử dụng nó trong việc phân tích và trực quan hoá dữ liệu, nhưng sử dụng nó trên web tiếp tục vẫn là một ứng dụng hấp dẫn và dễ hiểu nhất.

**3.2 Đồ thị tri thức trong việc tích hợp dữ liệu trong doanh nghiệp**

Tích hợp dữ liệu (Data Integration) là quá trình kết hợp dữ liệu từ nhiều nguồn khác nhau và cung cấp cho người dùng một cái nhìn tổng quát về dữ liệu.

Phần lớp dữ liệu doanh nghiệp nằm trong các cơ sở dữ liệu. Một cách tiếp cận trong việc tích hợp dữ liệu là dựa trên lược đồ toàn cục (global schema) để nắm bắt mối quan hệ qua lại giữa những thành phần dữ liệu được biểu diễn trên các cơ sở dữ liệu này. Hình thành một lược đồ toàn cục (global schema) là một quá trình thật sự khó khăn bởi vì có quá nhiều bảng và thuộc tính; những chuyên gia, những người mà tạo ra những cơ sở dữ liệu này không phải lúc nào cũng có mặt, và do sự thiếu thốn các tài liệu, nên khó để hiểu ý nghĩa của dữ liệu. Bởi vì thách thức trong việc hình thành một lược đồ toàn cục (global schema), nó sẽ thuận tiện hơn khi bỏ qua các vấn đề và chuyển đổi dữ liệu quan hệ (relational data) trong một cơ sở dữ liệu với một lược đồ bộ ba tổng quát, tức là đồ thị tri thức. Việc ánh xạ giữa những thuộc tính được tạo ra trên cơ sở cần thiết, ví dụ như để giải quyết các câu hỏi kinh doanh cụ thể và bản thân chúng có thể được biểu diễn trong một biểu đồ tri thức.

Nhiều tổ chức tài chính (financial institutions) quan tâm tới việc hình thành một đồ thị tri thức công ty, mà kết hợp được dữ liệu khách hàng nội bộ với dữ liệu có giấy phép từ các bên thứ ba. Một vài ví dụ về các kho dữ liệu bên thứ ba bao gồm Dunn & Bradstreet, S\&P 500, … Một ví dụ sử dụng một đồ thị tri thức công ty là trong việc đánh giá rủi ro trong khi đưa ra các quyết định cho vay. Dữ liệu bên ngoài bao gồm thông tin như các nhà cung cấp của một công ty. Nếu một công ty đang rơi vào tình trạng tài chính khó khăn, nó tăng rủi ro cho vay của các nhà cung cấp/ đầu tư của công ty đó. Để kết hợp dữ liệu bên ngoài này với dữ liệu nội bộ, người ta phải liên hệ được những lược đồ bên ngoài với lược đồ nội bộ công ty. Hơn nữa, tên công ty sử dụng trong các nguồn bên ngoài phải có mối quan hệ với định danh khách hàng tương ứng, được sử dụng bởi các tổ chức tài chính. Trong khi sử dụng một đồ thị tri thức là một hướng tiếp cận tích hợp dữ liệu, việc xác định các mối quan hệ có thể được hoãn lại cho đến khi chúng thật sự cần.

**4. Đồ thị tri thức trong Trí tuệ nhân tạo**

Đồ thị tri thức, hay được biết đến như mạng ngữ nghĩa (semantic network), đã được sử dụng trong việc biểu diễn trong Trí tuệ nhân tạo từ những ngày đầu tiên của lĩnh vực này. Trải qua nhiều năm, mạng ngữ nghĩa (semantic networks) được phát triển thành nhiều biểu diễn khác nhau như Conceptual Graphs, Description Logics và Rules Languages. Để nắm bắt những tri thức không chắc chắn, mô hình đồ thị xác suất (probabilistic graphical models) được phát minh.

Một ứng dụng được biết đến rộng rãi trong việc biểu diễn ngôn ngữ bắt nguồn từ mạng ngữ nghĩa (semantic networks) trong việc nắm bắt các Ontology (bản thể). Một Ontology là đặc tả (formal) chính thức về việc hình thành khái niệm của một miền (domain). Ontology đóng vai trò quan trọng trong trao đổi thông tin và trong việc nắm bắt tri thức tìm ân trong một miền có thể sử dụng cho việc luận và trả lời câu hỏi (answering question).

World Wide Web Consortium (W3C) được chuẩn hoá thành một họ của những biểu diễn tri thức ngôn ngữ mà bây giờ được sử dụng rộng rãi cho việc nắm bắt tri thức trên mạng Internet. Chúng ta sẽ đề cập một ngôn ngữ như thể trong phần tiếp theo, Resource Description Frame (RDF). Họ ngôn ngữ này bao gồm Web Ontology Language (OWL) và Semantic Web Rule Language (SWRL).

Giao hoà với việc biểu diễn tri thức, một thách thức chính trong AI là nút thắc thu nhận thông tin, tức là làm thế nào có thể nắm bắt tri thức trong biểu diễn được chọn trong một bối cảnh đang nở rộng. Những phương pháp tiếp cận sơ khai, dựa trên kỹ thuật tri thức (knowledge engineering). Cố gắng để tự động hoá các phần trong kỹ thuật tri thức dẫn đến những kỹ thuật như học quy nạp (inductive learning) và thế hệ hiện tại của Máy học.

Do đó, như một điều tự nhiên, đồ thị tri thức được sử dụng như một biểu diễn được lựa chọn trong lữu trữ tri thức được học một cách tự động. Ngày càng có nhiều sự quan tâm đến việc tận dụng miền tri thức được thể hiện trong đồ thị tri thức để cải thiện Máy học.

**4.1 Đồ thị tri thức như đầu ra của Máy học**

Chúng ta sẽ xem xét làm thế nào mà đồ thị được sử dụng như là một mục tiêu biểu diễn đầu ra trong các thuật toán Xử lý ngôn ngữ tự nhiên và Thị giác máy tính.

Rút trích thực thể và rút trích quan hệ từ văn bản là hai tác vụ cơ sở trong Xử lý ngôn ngữ tự nhiên. Việc rút trích thông tin từ nhiều phần trong văn bản cần có mối tương quan và đồ thị tri thức cung cấp một phương tiện tự nhiên để thực hiện mục đích như vậy.

Ví dụ, từ một câu như sau:

“Albert Einstein was a German-born theoretical physicist who developed the theory of relativity.”

Chúng ta có thể rút trích những thực thể Albert Einstein, Germany, Theoretical Physicist, và Theory of Relativity, những quan hệ born in, occupation and developed.

Khi đoạn trích này của đồ thị tri thức được kết hợp vào một đồ thị tri thức lớn hơn, chúng ta sẽ nhận được các liên kết bổ sung (được hiển thị bằng các cạnh chấm chấm), chẳng hạn như Nhà vật lý lý Thuyết (Theoretical Physicist) là một loại Nhà vật lý (Physictist), nghiên cứu Vật lý và Lý Thuyết Tương Đối (Theory of Relativity) là một nhánh của Vật lý.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-25-what-is-knowled-graph/media/image2.png)

Thị giác máy tính (Nguyên văn: A holy grail of Computer vision, :))chén thánh này vjp pro quá mình cũng khum biết nói sao, hj\!) là sự hiểu biết về hình ảnh, hình thành một mô hình, mà có thể định danh, nhận diện vật thể (detect objects), mô tả thuộc tính (attributes) của chúng, và nhận dạng quan hệ của chúng. Sự hiểu biến về khung cảnh thế giới cho cho phép các ứng dụng quan trọng như tìm kiếm hình ảnh (image search), trả lời câu hỏi (question answering) và tương tác với robot (robotic interactions). Nhiều tiến bộ đã đạt được trong những năm gần đây hướng tới mục tiêu này, bao gồm phân loại hình ảnh (image classification) và phát hiện đối tượng (object detection).

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-25-what-is-knowled-graph/media/image3.png)

Lấy ví dụ, từ một ảnh phía trên, một hệ thống tri thức hình ảnh nên tổ chức một đồ thị tri thức như phía bên phải. Các nút (node) trong đồ thị tri thức là đầu ra của một bộ phát hiện đối tượng. Những nghiên cứu gần đây trong Thị giác máy tính đang tập trung vào phát triển những kỹ thuật có thể dự đoán chính xác mối quan hệ giữa những đối tượng, ví dụ như, người đàn ông kia đang cần một cái xô, và chú ngựa đang ăn từ cái xô đó, … Đồ thị tri thức ở bên phải là một ví dụ của một đồ thị tri thức (tui hơi lú rồi)

**4.2 Đồ thị tri thức như đầu vào của Máy học**

Những mô hình máy học sâu phổ biến (Deep Machine Learning Models) dựa trên đầu vào dữ liệu số, những ký hiệu hoặc cấu trúc rời rạc trước tiên nên được chuyển đổi về dạng biểu diễn số. Embeddings (nhúng, nghe chuối quá, nên mình giữa lại nguyên gốc) biến đổi một ký tự đầu vào thành một vector (mảng nếu 1 chiều, ma trận nếu 2 chiều, tổng quát thì tensor) số học như một biểu diễn đã trở thành sự lựa chọn cho những mô hình máy học. Chúng ta sẽ giải thích những khái niệm này và mối quan hệ của nó với đồ thị tri thức bằng cách lấy ví dụ về word embeddings và graph embeddings.

Word embeddings được phát triển cho việc tính toán độ tương đồng giữa những từ. Để hiểu word embeddings, chúng ta xem xét một tập những câu sau đây:

I like knowledge graphs.

I like databases.

I enjoy running.

Trong những câu trong tập hợp trên, chúng ta sẽ đếm xem một từ xuất hiện kế bên một từ cách bao nhiêu lần và lưu lại kết quả vào một ma trận. Ví dụ, từ I xuất hiện kế bên từ like hai lần, kế bên từ enjoy một lần và không lần với tất cả những từ còn lại

|           |   |      |       |           |        |           |         |   |
| --------- | - | ---- | ----- | --------- | ------ | --------- | ------- | - |
| counts    | I | like | enjoy | knowledge | graphs | databases | running | . |
| I         | 0 | 2    | 1     | 0         | 0      | 0         | 0       | 0 |
| like      | 2 | 0    | 0     | 1         | 0      | 1         | 0       | 0 |
| enjoy     | 1 | 0    | 0     | 0         | 0      | 0         | 1       | 0 |
| knowledge | 0 | 1    | 0     | 0         | 1      | 0         | 0       | 0 |
| graphs    | 0 | 0    | 0     | 1         | 0      | 0         | 0       | 1 |
| databases | 0 | 1    | 0     | 0         | 0      | 0         | 0       | 1 |
| running   | 0 | 0    | 1     | 0         | 0      | 0         | 0       | 1 |
| .         | 0 | 0    | 0     | 0         | 1      | 1         | 1       | 0 |

Chúng ta nói rằng ý nghĩa của mỗi từ được biểu diễn bởi vector dòng tương ứng với từ đó. Để tính toán độ tương đồng giữa các từ, chúng ta có thể dễ dàng tính toán độ tương đồng giữa những vectors tương ứng với chúng. Trong thực tế, chúng ta quan tâm trong văn bản mà có thể chứa hàng triệu từ và hy vong có biểu diễn thể biểu diễn gọn hơn. Vì ma trận trên là một ma trận thưa, chúng ta có thể sử dụng những kỹ thuật từ Đại số Tuyến tính (như, SVD - singular value decompsition) để giảm chiều dữ liệu. Kết quả cho ra vector tương ứng với từ được gọi là word embedding. Thông thường thì word embedding sử dụng trong ngày nay dựa trên những vectors có độ dài khoảng 200.

Có rất nhiều biến thể và phần mở rộng của ý tưởng cơ bản được trình bày ở đây. Các kỹ thuật tồn tại để tự động học word embedding cho bất kỳ văn bản nhất định nào.

Việc sử dụng word embedding cải thiện hiệu suất của rất nhiều tác vụ Xử lý ngôn ngữ tự nhiên bao gồm rút trích thực thể (entity extraction), rút trích quan hệ (relation extraction), phân tích cú pháp (parsing), truy xuất văn bản (passage retrieval), … Một trong những ứng dụng phổ biến nhất của word embedding là trong tự động hoàn thành các câu truy vấn tìm kiếm. Word embedding cung cấp cho chúng ta một cách dễ dàng trong việc dự đoán các từ có khả năng tuần theo truy vấn một phần mà người dùng nhập

Một văn bản là một chuỗi của những từ, và word embeddings tính toán đồng hiện (co-occurrences) cửa những từ trong đó, chúng ta có thể quan sát văn bản như một đồ thị tri thức mà mỗi từ là một nút (node) và những cạnh liên kết có hướng giữa mỗi từ này với từ khác. Graph Embeddings tổng quát hoá khái niệm này cho một cấu trúc mạng tổng quát. Mục đích và tiếp cận, tuy nhiên vẫn tiếp tục giống nhau: biểu diễn mỗi node trong một đồ thị tri thức bởi một vector, do đó độ tương đồng giữa những node có thể được tính toán như một hiệu giữa các vector tương ứng với chúng. Những vector cho mỗi node được gọi là Graph Embeddings

Để tính toán knowledge graph embedding, chúng ta định nghĩa một phương thức cho việc mã hoá mỗi nút trong một đồ thị thành một vector, một hàm để tính toán độ tương đồng giữa những nút (node), sau đó tối ưu hàm mã hoá (encoding function). Việc mã hoá một nút thành một vector được gọi là node embedding . Một hàm mã hoá có thể được sử dụng là random-walk của đồ thị tri thức (thường là 32 đến 64 random-walk) và tính toán đếm đồng hiện của những node trong đồ thị tri thức tạo ra một ma trận tương tự như đếm đồng hiện của những từ trong văn bản. Có rất nhiều phương pháp cơ bản để tính toán knowledge graph embedding. Giống như chúng ta muốn mã hoá một node thành một vector, chúng ta cũng có thể mã hoá toàn bộ đồ thị thành một vector, mà được hiểu là graph embedding. Ở đây có nhiều tiếp cận tính toán graph embedding, nhưng có lẽ tiếp cận đơn giản nhất là thêm vector cho mỗi node trong đồ thị và thu được một vector biểu diễn cho toàn bộ đồ thị.

Giải thích graph embedding bằng cách giải tính word embedding trước tiên là cách dễ nhất để hiểu chúng và cách sử dụng của chúng. Graph Embedding là một trường hợp tổng quát cho word embeddings. Chúng là một con đường để một đầu vào tri thức thể hiện trong một đồ thị tri thức vào một thuật toán Máy học. Graph Embeddings không quy nạp biểu diễn tri thức, mà là cách biến biểu diễn ký hiệu thành biểu diễn số để dùng cho một thuật toán Máy học.

Chúng ta tính toán knowledge graph embeddings một lần, chúng có thể được sử dụng cho rất nhiều ứng dụng. Một cách sử dụng rõ ràng của knowledge graph embeddings được tính toán từ đồ thị tình bạn là giới thiệu những người bạn mới. Một nhiệm vụ nâng cao hơn liên quan đến dự đoán liên kết (tức là khả năng liên kết giữa hai nút). Dự đoán liên kết trong biểu đồ công ty có thể được sử dụng để xác định khách hàng mới tiềm năng.

**5. Tổng kết**

Đồ thị là một cấu trúc cơ bản trong Toán học Rời Rạc (Discrete Mathematics) và có nhiều ứng dụng trong nhiều lĩnh vực của Khoa học Máy tính (Computer Science). Công dụng đáng chú ý của đồ thị trong biểu diễn tri thức và cơ sở dữ liệu tri thức ở dạng dữ liệu đồ thị (data graphs), taxonomies, ontologies. Một cách truyền thống, những ứng dụng như thế này dựa trên thiết kế top down. Như một đồ thị tri thức (knowledge graph) là một đồ thị hữu hướng được gán nhãn (Directed Labeled Graphs), chúng ta có thể tận dụng lý thuyết. thuật toán và cài đặt từ nhiều hệ thống dựa trên đồ thị trong Khoa học Máy tính.

Sự gia tăng gần đây trong việc sử dụng đồ thị tri thức dựa trên ba tiến bộ khác nhau:

\- (1) Dữ liệu liên kết và chia sẻ trên web

\- (2) Tính toán đồ thị trên dữ liệu

\- (3) Những quá trình trong Xử lý ngôn ngữ tự nhiên và Thị giác để rút trích quan hệ từ văn bản và hình ảnh

Một điểm chung giữa ba tiến bộ này là quy mô. Đồ thị tri thức hiện nay có quy mô chưa từng có. Chúng ta đã chú nhận thấy rằng một phiên bản gần đây của Wikidata đã có hơn 80 triệu đối tượng, và hơn 1 tỉ quan hệ. Nhiều đồ thị tri thức công nghiệp ngày càng lớn hơn, lấy ví dụ như, một phiên bản gần đây của đồ thị tri thức Google đã có hơn 570 triệu thực thể, và hơn 18 tỉ quan hệ. Quy mô lớn của đồ thị tri thức tạo ra sự hiệu quả và khả năng mở rộng của các thuật toán đồ thị là điều tối quan trọng.

Việc tổ chức thông tin trên web, và trong nhều ứng dụng tích hợp dữ liệu, nó thật sự khó để đưa ra một thiết kế top-down của một lược đồ. Các ứng dụng Máy học dựa trên dữ liệu có sẵn mà có thể dự đoán hữu ích từ nó. Những sử dụng bottom-up của đồ thị tri thức không làm giảm giá trị của thiết kế từ trên xuống của lược đồ hoặc ontology. Thật vậy, dự án Wikidata tận dụng các ontology. để đảm bảo chất lượng dữ liệu, và hầu hết các dự án tích hợp dữ liệu doanh nghiệp ủng hộ việc xác định lược đồ trên cơ sở cần thiết. Ứng dụng Máy học cũng hưởng lợi ích đáng kể với việc sử dụng nguồn onotology dồi dào cho việc tạo ra các suy diễn từ thông tin mà đã học được cho dù một ontology toàn cục hay một lược đồ không yêu cầu ngay từ đầu.

Word-Embeddings và Graph-Embedding tận dụng cấu trúc một đồ thị trong dữ liệu đầu vào, nhưng chúng cần phải tổng quát hơn đồ thị tri thức ở chỗ không rõ ràng và rõ ràng cho một lược đồ hay một ontology. Ví dụ, graph embeddings có thể được sử dụng trên khắp mạnh được định nghĩa bởi trao đổi gói tin giữa các nút trên mạng Internet, và sau đó được sử dụng trong các thuật toán máy học để dự đoán các nút mạo danh. Ngược lại, với đồ thị tri thức Wikidata, đồ thị tri thức trong doanh nghiệp, và trong biểu diễn đầu ra của các thuật toán máy học, một lược đồ hay ontology có thể đóng vai trò trung tâm.

Chúng ta kết lại bằng cách quan sát sự gia tăng quan tâm về đồ thị tri thức gần đây chủ yếu được thúc đẩy bởi các yêu cầu bottom-up của một số ứng dụng kinh doanh hấp dẫn. Đồ thị tri thức trong những ứng dụng này có thể chắn chắn hưởng lợi ích từ những công trình kinh điển từ những kỹ thuật thiết kế biểu diễn top-down, và thực tế, chúng ta có thể hình dung rằng cả hai hướng này sẽ cùng hội tụ với nhau.

**Bài tập:**

...Sẽ cập nhật sau…

Bài giảng gốc: [https://web.stanford.edu/class/cs520/2020/notes/What\_is\_a\_Knowledge\_Graph.html]()
