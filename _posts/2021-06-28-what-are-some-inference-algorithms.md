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

# WHAT ARE SOME KNOWLEDGE GRAPH INFERENCE ALGORITHMS

MỘT SỐ THUẬT TOÁN SUY DIỄN ĐỒ THỊ TRI THỨC

## 1\. Giới thiệu

Khi chúng ta đã khởi tạo đồ thị tri thức, chúng quan tâm đến truy xuất thông tin, và sử dụng những thông tin đó để đưa ra những kết luận mới. Chúng ta đã giới thiệu qua những ngôn ngữ truy vấn (query languages) mà chúng ta có thể sử dụng để thực hiện truy xuất trên đồ thị. Trong chương này, chúng ta sẽ tập trung vào những thuật toán suy diễn, vượt ra ngoài truy xuất, tức là kết luận những dữ kiện mới từ đồ thị tri thức mà không được biểu diễn một cách rõ ràng trong đó. Các thuật toán suy diễn có thể được gọi thông qua giao diện khai báo truy vấn.

Chúng ta sẽ đề cập hai lớp lớn của các thuật toán suy luận: Graph Algorithms - Các thuật toán đồ thị, và Ontology-Based Algorithm - Các thuật toán dựa trên Ontology. Các thuật toán đồ thị (Graph Algorithms) có thể được áp dụng cho bất kỳ dữ liệu cấu trúc đồ thị (graph-structured data) nào, và hỗ trợ nhiều toán tử như tìm đường đi ngắn nhất giữa các nút trong đồ thị (finding minimum paths between nodes in a graph), xác định các nút quan trong trong một đồ thị (identifying salient nodes in a graph). Các thuật toán dựa trên Ontology thực hiện trên cấu trúc đồ thị nhưng tính đến ngữ nghĩa của nó, ví dụ như, duyệt đường đi cụ thể, hay kết luận những liên kết mới dựa trên miền tri thức nền tảng (background domain knowledge). Trong chương này, chúng ta sẽ đề cập cả hai lớp thuật toán trên.

Về nguyên tắc, chúng ta có thể gọi những thuật toán đồ thị, và những thuật toán suy luận dựa trên Ontology thông qua một giao diện khai báo truy vấn (declarative query interface) của những loại mà chúng ta đã đề cập trước đó. Suy luận dựa trên Ontology có thể tận dụng được những thuật toán dựa trên đồ thị. Ví dụ như, kiểm tra nếu một đối tượng A là một thể hiện của một lớp B, có thể hoàn thành kiểm tra bằng cách kiểm tra liệu có tồn tại hay không một đường đi trong một lớp nằm giữa C và B trong đó C là trung gian của A.

## 2\. Các thuật toán suy luận dựa vào đồ thị - Graph-based Inference Algorithms

Chúng ta sẽ đề cập ba lớp thuật toán lớn trong những thuật toán đồ thị:

\- (1) Path finding - Tìm kiếm đường đi

\- (2) Centrality detection - Xác định trung tâm

\- (3) Community detection - Xác định quần thể (cộng đồng)

Tìm kiếm đường đi - Path finding liên quan đến việc tìm kiếm một đường đi nằm giữa hai hay nhiều nút trong một đồ thị mà đáp ứng những thuộc tính nhất định.

Xác định (Nhận diện) trung tâm - Centrality detection là về những hiểu biết mà những nút là quan trọng trong một đồ thị. Những phương thức khác nhau được sử dụng để xác định ý nghĩa quan trọng dẫn đến rất nhiều biến thể trong những thuật toán xác định (nhận diện) trung tâm - Centrality detection algorithms.

Và cuối cùng, community detection - xác định (nhận diện) cộng đồng là việc định danh một nhóm các nút (a group of nodes) trong một đồ thị mà đáp ứng được một vài tiêu chí để nằm trong cùng một cộng đồng (quần thể, lớp). Community detection - xác định (nhận diện) cộng đồng rất hữu ích trong việc nghiên cứu những hành vi mới nổi (emergent behaviors) trong một đồ thị mà có thể không được chú ý đến.

Chúng ta sẽ đề cập mỗi một loại trong những thuật toán đồ thị chi tiết hơn. Với mỗi loại, chúng ta sẽ trình bày tổng quan, thảo luận những cách khác nhau rất hữu ích, và xem xét một vài ví dụ cho các thuật toán.

### 2.1 Các thuật toán tìm đường đi - Path Finding Algorithms

Có rất nhiều biến thể của vấn đề tìm kiếm đường đi trong một đồ thị: tìm đường đi ngắn nhất giữa hai nút cho trước (finding the shortest path between any given two nodes), tìm đường đi ngắn nhất giữa tất cả các cặp nút (finding the shortest paths between all pairs of nodes), tìm một cây khung nhỏ nhất (finding a minimum spanning tree). Đường đi ngắn nhất trong một đồ thị (The shortest path in a graph) là một đường đi giữa hai nút trong một đồ thị mà tổng trọng số của các cạnh liên kết là nhỏ nhất. Nếu không có trọng số gắn với một cạnh liên kết, thì nó được giả định là 1. Đường đi ngắn nhất giữa hai nút bất kỳ có thể được sử dụng trong lập kế kế hoạch tối ưu định tuyến trong một hệ thống điều hướng giao thông. Một cây khung nhỏ nhất (A minimum spanning tree) tính toán chi phí ít nhất cho việc đi đến tất cả các nút trong một tập các nút, có thể hữu ích trong vấn đề lập kế hoạch tham quan, du dịch.

Như một ví dụ về một thuật toán tìm đường đi ngắn nhất đặc biệt, chúng ta sẽ đề cập đến thuật toán $A^{\*}$ (the $A^{\*}$ Algorithm) mà là một trường hợp tổng quát của thuật toán Dijkastra's Algorithm. Thuật toán $A^{\*}$ cũng được sử dụng rộng rãi như một thuật toán tìm kiếm để giải quyết những vấn đề lập lịch AI (solving AI Planning problems).

Thuật toán $A^{\*}$ thực hiện duy trình một cây những đường đi có gốc tại nút bắt đầu và mởi rộng những đường đi này từng cạnh một cho đến khi điều kiện dừng của nó được thoã mãn. Ở mỗi bước, nó quyết định đường đidựa trên chi phí đường đi cho đến hiện tại và ước lượng chi phí cần để mở rộng tất cả con đường đi đến đích. Nếu $n$ là nút kế tiếp để ghé thăm, $g(n)$ chi phí cho đến hiện tại, và $h(n)$ ước lượng chi phí cần thiết để mở rộng đường đi đến đích, sau đó nó chọn nút mà tối tiểu được $f(n)$, trong đó $f(n) = g(n) + h(n)$.

Chúng ta phải chọn một admissible heuristic (heuristic có thể chấp nhận được) sao cho nó không bao giờ ước tính quá mức chi phí để đạt được mục tiêu. Trong một biến thể, được gọi là Best First Search, heuristic chọn đường đi mới chi phí tổng cộng thấp nhất cho đến hiện tại, tức là, nó đặt $h(n) = 0$. Cũng tồn tại tài liệu chuyên sâu về những heuristic khác nhau mà có thể được dùng trong tìm kiếm $A^{\*}$.

### 2.2 Các thuật toán xác định trung tâm - Centrality Detection Algorithms

Các thuật toán xác định trung tâm - The centrality detection algorithms được sử dụng để hiểu tốt hơn những vai trò được đảm nhận bởi các nút khác nhau trên toàn bộ đồ thị. Phân tích này có thể giúp chúng ta hiểu biết những nút quan trọng nhất trong một đồ thị, tính linh động của một nhóm và khả năng bắc cầu (nối) giữa những nhóm (groups) với nhau.

Có rất nhiều biến thể của thuật toán xác định trung tâm (Centrality Detection Algorithms): degree centrality, closeness centrality, between-ness centrality, và page rank.

Degree centrality đơn giản là đếm số những cạnh ra/ vào (incoming and/or outgoing edges). Một nút với một ra cao (a high outgoing degree) trong mạng lưới chuỗi cung ứng(supply chain network) gợi ý đó là một nhà cung ứng độc quyền (a supplier monopoly).

Closeness centrality xác định những nút mà có đường đi ngắn nhất đến tất cả các nút khác. Với những thông tin như vậy có thể hữu ích trong việc xác định vị trí cho một dịch vụ mới để mà nó có thể tiếp cận phạm vi khách hàng rộng nhất.

Between-ness centrality xác định một nút dựa trên số con đường đi ngắn nhất giữa các nút đi qua nó. Between-ness centrality là một độ đo phạm vi ảnh hưởng bởi những nút trong một mạng.

Cuối cùng, thuật toán PageRank (the PageRank Algorithm) đo mức độ quan trọng của một nút dựa trên những nút khác mà liên kết đệ quy.

Trong phần thảo luận này, chúng ta sẽ đề cập thuật toán PageRank một cách chi tiết hơn. Ban đầu PageRank được phát triển cho việc xếp hạng (ranking) những trang web cho WWW Search (Tìm kiếm WWW). Nó cho phép đo ảnh hưởng bắc cầu (transitive influence) trên một nút. Ví dụ như, một nút liên kết với một vài nút rất quan trọng có thể quan trọng hơn nút mà liên kết với một lượng lớn các nút không quan trọng. Chúng ta có thể định nghĩa PageRank của một nút như sau:

$PR(u) = (1- d) + d \\times \\left(\\frac{PR(T\_1)}{C(T\_1)} + ... + \\frac{PR(T\_n)}{C(T\_n)}\\right)$

Trong biểu thức ở trên, chúng ta giả định rằng nút $u$ có những cạnh vào từ những nút $T\_1, T\_2, …, T\_n$. Chúng ta sử dụng $d$ như một damping factor - hệ số đệm mà thường được đặt là $0.85$. $C(T\_1), C(T\_2), …, C(T\_n)$ là số cạnh vào từ những nút $T\_1, T\_2, …, T\_n$. Thuật toán thực hiện một cách tuần tự bằng cách đầu tiền cài đặt PageRank cho tất cả các nút về cùng một giá trị, và sau đó tuần tự cải thiện nó với một số lần duyệt cố định, cho đến khi những giá trị này hội tụ.

Ngoài phiên bản gốc của nó được sử dụng trong việc xếp hạn các kết quả tìm kiếm cho những truy vấn WWW, PageRank cho thấy nhiều ứng dụng thú vị khác. Ví dụ như, nó được sử dụng trên các trang phương tiện xạ hội (social media sites) để gợi ý cho một người dùng cụ thể nên theo dõi ai. Nó cũng được sử dụng trong phân tích gian lân (fraud analysis) để xác định những hoạt động bất thường với những nút trong một đồ thị.

### 2.3 Các thuật toán xác định cộng đồng - Community Detection Algorithms

Nguyên lý chung cơ bản cho những thuật toán xác định cộng đồng (The general principle underlying the community detection algorithms) là những nút mà nằm trong một công đồng có nhiều quan hệ trong cộng đồng hơn những nút nằm ngoài cộng đồng đó. Đôi khi, phân tích cộng đồng (Community Analysis) có thể là bước phân tính đầu tiên trong một đồ thị để mà một phân tích sâu hơn có thể được thực hiện với những nút trong cộng đồng.

Có nhiều thuật toán xác định cộng đồng khác nhau - Community Detection Algorithm như: connected components, strongly connected components, label propagation và fast unfolding (cũng được gọi là Louvain algorithm)

Hai thuật toán đầu tiên trong số các thuật tán, connected components - thành phần liên thông, strongly connected components - thành phần liên thông mạnh thường được sử dụng trong những phân tích khởi đầu cho một đồ thị. Thuật toán thành phần liên thông (Connected Components Algorithm) và thuật toán thành phần liên thông mạnh (Strongly Connected Components Algorithm) là những kỹ thuật chuẩn trong Lý thuyết Đồ thị (Graph Theory). Một thành phần liên thông (A connected component) là một tập các nút mà có một đường đi giữa hai nút bất kỳ trong một đồ thị vô hướng. Một thành phần liên thông mạnh (A strongly connected component) là một tập các nút mà với bất kỳ nút A và B nào trong tập hợp, tồn tại một đường đi nối từ nút A đến nút B và đường đi từ nút B đến nút A.

Cả label propagation - Nhãn lan truyền và fast unfolding là những thuật toán bottom-up cho việc xác định cộng đồng trong một đồ thị lớn. Chúng ta sẽ xem xét cả hai thuật toán này chi tiết hơn.

Label propagation bắt đầu bằng việc gán cho mỗi nút trong một đồ thị một cộng đồng khác nhau. Sau đó, chúng ta sắp xếp các nút một cách ngẫu nhiên để cập nhật cộng đồng của chúng như sau. Chúng ta kiểm tra những nút theo thứ tự được chỉ định, với mỗi nút, chúng ta kiểm ra láng giềng của nó và đặt cộng đồng nó cho cộng đồng được chia sẻ bởi phần lớn láng giềng của nó. Các mối quan hệ bị phá vỡ một cách ngẫu nhiên đồng nhất. Thuật toán dừng khi mỗi nút được gán cho một cộng đồng được chia sẻ bởi phần lớn láng giềng của nó. :v?

Trong thuật toán Fast Unfolding, có hai giai đoạn. Chúng ta khởi tạo mỗi một nút là một cộng đồng riêng biệt. Trong giai đoạn đầu tiên, chúng ta kiểm tra mỗi nút và mỗi láng giềng của nó và đánh giá liệu có bất kỳ lợi ích tổng thể nào khi tính mô-đun khi đặt nút này vào cùng một cộng đồng với một láng giềng hay không. Một độ đo để tính toán mô-đun được định nghĩa. Nếu không có lợi ích nào, nút sẽ rời khởi cộng đồng ban đầu của nó. Trong giai đoạn thứ hai của thuật toán, chúng ta khởi tạo một mạng mới trong đó một nút tương ứng với mỗi cộng đồng từ giai đoạn 1, và một cạnh liên kết giữa hai nút nếu có một canh liên kết giữa vài nút trong những cộng đồng giai đoạn 1 tương ứng của chúng. Liên kết giữa những nút trong cùng một cộng đồng trong giai đoạn 1 dẫn đến các khuyên (self-loops) cho nút tương ứng với cộng đồng của chúng trong giai đoạn 2. Khi giai đoạn hai hoàn tất, thuật toán lặp lại bằng cách áp dụng giai đoạn 1 lên đồ thị kết quả.

Một ví dụ về một hàm tính toán mô-đun (a modularity function) được sử dụng trong thuật toán ở bên trên

$Q = \\sum\_{i=1}^k\\left\[\\frac{e\_i}{m} - \\left(\\frac{d\_i}{2m}\\right)^{2}\\right\]$

Trong biểu thức trên, chúng ta tính toán được điểm tổng mô-đun (overall modularity score) Q của một mạng được phân tách thành $k$ cộng đồng, trong đó $e\_i$ và $d\_i$ là tương ứng với số nút, và tổng bậc các nút trong cộng đồng $i$m và $m$ là tổng số cạnh trong mạng.

Cả label propagation algorithm và fast unfolding algorithm cho ra những chi tiết về cộng đồng mới nổi (emergent communities) và những tìm ẩn ngoài dự kiến (potentially unanticipated). Việc thực hiện khác nhau cũng có thể dẫn đến việc xác định các cộng đồng khác nhau.

## 3\. Các thuật toán suy luận dựa trên Ontology - Ontology-based Inference Algorithms

Suy luận dựa trên Ontology phân biệt một hệ thống đồ thị tri thức (knowledge graph system) với một hệ thống suy luận dựa trên đồ thị tổng quát (general graph-based system). Chúng ta sẽ phân loại suy diễn dựa trên Ontology thành hai loại:

\- (1) Taxonomic Inference - Suy luận phân loại

\- (2) Rule-based inference - Suy luận dựa trên luật

Suy luận phân loại (Taxonomic Inference) chủ yếu dựa trên phân cấp các lớp (hierarchy of classes) và thể hiện (instances) và kế thừa (inheritance) của những giá trị qua những cấp bậc. Suy luận dựa trên luật (Rule-based inference) có thể liên hệ với những luật logic tổng quát. Chúng ta có thể truy cập suy luận Ontology thông qua một giao diện khai báo truy vấn, và do đó, nó có thể được sử dụng như một dịch vụ suy luận chuyên biệt (specialized reasoning service) cho một lớp truy vấn xác định.

### 3.1 Taxonomic Reasoning - Suy diễn phân loại

Taxonomic reasoning - Suy diễn phân loại được áp dụng trong những tình huống mà nó có ích trong việc tổ chức tri thức thành những lớp (classes). Chúng ta sẽ đề cập những khái niệm về class membership, class specialization, disjoint classes, value restriction, inheritance và various inferences có thể được rút ra suy luận bằng cách sử dụng chúng.

Cả đồ thị thuộc tính (Property Graph) và mô hình dữ liệu RDF (RDF Data Model) đều hỗ trợ lớp. Với đồ thị thuộc tính, kiểu các nút tương đương với lớp. Với RDF, có một mở rộng gọi là RDF Schema - Lược đồ RDF mà hộ trợ định nghĩa các lớp. Trong một mở rộng cao cấp hơn của RDF như Web Ontology Language và Semantic Web Rule Language, một sự hỗ trợ đầy đủ sẵn có cho việc định nghĩa các lớp và các luật.

Để thảo luận Taxonomic Reasoning, chúng ta chọn cách giới thiệu ra khỏi đồ thị thuộc tính (Property Graph) và mô hình dữ liệu RDF (RDF Data Model). Chúng ta sẽ giới thiệu những khái niệm cơ bản của taxonomies như class membership, disjointness, constraints và inheritance bằng cách sử dụng Datalog như một ngôn ngữ đặc tả ( a specification language).

#### 3.1.1 Class Membership - Lớp Membership

Giả sử chúng ta mong muốn mô hình hoá dữ liệu về quan hệ họ hàng (kinship). Chúng ta có thể định nghĩa những quan hệ một ngôi (unary relations) của male và female như những lớp, có những thành viên như art, bob, bea, coe, … Những thành viên của một lớp được coi như một thể hiện của lớp đó.

Đối với mỗi vị từ một ngôi mà chúng tôi cũng muốn tham chiếu đến như một lớp, chúng ta thêm một đối tượng không đổi (object constant) với cùng tên với tên của quan hệ không đổi (relation constant) như sau

|             |               |
| ----------- | ------------- |
| class(male) | class(female) |

Do vậy, male vừa là một đối tượng không đổi (object constant) vừa là quan hệ không đổi (relation constant) . Đây là một ví dụ về cách dùng của *metaknowledge* và đôi khi nó cũng được gọi là punning.

Để biểu diễn art là một thể hiện của lớp male, chúng ta thêm vào một quan hệ gọi là instance\_of và sử dụng nó như sau:

|                        |                           |
| ---------------------- | ------------------------- |
| instance\_of(art,male) | instance\_of(bea,female)  |
| instance\_of(bob,male) | instance\_of(coe,female)  |
| instance\_of(cal,male) | instance\_of(cory,female) |
| instance\_of(cam,male) |                           |

#### 3.1.2 Class Specialization - Lớp Specialization

Những lớp có thể được tổ chức thành dạng hệ thống phân cấp. Ví dụ, chúng ta có thể thêm vào một lớp person. Cả male và female bây giờ là lớp con - subclass của person

|                           |                             |
| ------------------------- | --------------------------- |
| subclass\_of(male,person) | subclass\_of(female,person) |

Quan hệ subclass\_of là quan hệ bắc cầu, tức là nếu A là một lớp con (subclass) của B, và B là một lớp con (subclass) của C, thì A là một lớp con (subclass) của C. Lấy ví dụ, nếu mother là một lớp con của female, thì mother cũng là một lớp con của person.

|                                                            |
| ---------------------------------------------------------- |
| subclass\_of(A,C) :- subclass\_of(A,B) & subclass\_of(B,C) |

Những quan hệ subclass\_of và instance\_of được liên hệ trong đó, nếu A là một lớp con của Bm thì tất cả những thể hiện của A cũng là thể hiện của B. Trong ví dụ của chúng ta, tất cả những thể hiện của male cũng là tất cả những thể hiện của person.

|                                                            |
| ---------------------------------------------------------- |
| subclass\_of(I,B) :- subclass\_of(A,B) & instance\_of(I,A) |

Một hệ thống phân cấp lớp (Class hierarchy) không được chứa các chu trình (cycles) bởi vì điều đó có nghĩa rằng một lớp là một lớp con của chính nó, điều này không chính xác về mặt ngữ nghĩa. (Cũng dễ hiểu)

#### 3.1.3 Class Disjointness - Lớp Disjointness

Chúng ta nói rằng một lớp A là disjoint - tách rời với một lớp khác là B nếu không có thể hiện nào của một trong số chúng là thể hiện của một lớp kia. Chúng ta có thể khai báo hai lớp là tách rời với nhau hoặc một tập hợp các lớp là một phân vùng sao cho mỗi lớp trong tập đó là tách rời từng cặp với mọi lớp khác. Trong ví dụ quan hệ họ hàng, lớp make và female tách rời với nhau:

|                                                          |
| -------------------------------------------------------- |
| \~instance\_of(I,B) :- disjoint(A,B) & instance\_of(I,A) |
| \~instance\_of(I,A) :- disjoint(A,B) & instance\_of(I,B) |
| disjoint(A1,A2) :- partition(A1,...,An)                  |
| disjoint(A2,A3) :- partition(A1,...,An)                  |
| disjoint(An-1,An) :- partition(A1,...,An)                |

#### 3.1.4 Class Definition - Lớp Definition

Những lớp được định nghĩa bằng cách sử dụng những giá trị quan hệ *necessary* (cần) và *sufficient* (đủ). Ví dụ: age (tuổi) là giá trị quan hệ cần thiết cho một người. Nếu chúng ta định nghĩa một lớp người tóc nâu (a brown-haired person), điều đó là cần (necessary) và đủ (sufficient) cho một người có tóc màu nâu trở thành một thể hiện của lớp này:

<table>
<tbody>
<tr class="odd">
<td><p>instance_of(X,brown_haired_person) :-</p>
<p>instance_of(X,person) &amp; has_hair_color(X,brown)</p></td>
</tr>
</tbody>
</table>

Lớp chỉ có những giá trị quan hệ cần thiết được gọi là *primitive* classes - lớp nguyên thuỷ và lớp mà chúng ta biết được cả những giá trị cần và đủ được gọi là *defined* classes. Định nghĩa đủ của một lớp có instance\_of trong phần đầu của nó

#### 3.1.5 Value Restriction - Giới hạn giá trị

Chúng ta có thể giới hạn các đối số của một quan hệ mà là thể hiện của những lớp xác định. Trong ví dụ quan hệ họ hàng, chúng ta có thể giới hạn giá trị của quan hệ parent để mà những đối số của nó luôn luôn là thể hiện của lớp person. Do vậy, nếu một lập luận yêu cầu chứng minh parent(table, chair), nó có thể kết luận đơn giản là không đúng bằng cách nhận thấy cả table và chair không là thể hiện của person. Giới hạn trên đối số đầu tiên của một quan hệ thường được gọi là một miền giới hạn (a domain restriction) và giới hạn trên đối số thức hai của một quan hệ được gọi là khoảng giới hạn (range restriction). Tương tự, giới hạn có thể được định nghĩa cho những mối quan hệ đa ngôi.

|                                                                           |
| ------------------------------------------------------------------------- |
| illegal :- domain(parent,person) & parent(X,Y) & \~instance\_of(X,person) |
| illegal :- range(parent,person) & parent(X,Y) & \~instance\_of(Y,person)  |

#### 3.1.6 Cardinality and Number Consraints - Các ràng buộc về số lượng và số học

Chúng ta có thể giới hạn nhiều hơn những giá trị của những quan hệ bằng cách xác định những ràng buộc số lượng và số học. Một ràng buộc số lượng giới hạn số lượng của một mối quan hệ và một ràng buộc số học xác định khoảng giá trị số học mà một quan hệ có thể có. Ví dụ như, chúng ta có thể nói rằng một người có chính xác hai phụ huynh, và tuổi của một người nằm giữa 0 và 100 năm.

|                                                                   |
| ----------------------------------------------------------------- |
| illegal :- instance\_of(X,person) & \~countofall(P,parent(P,X),2) |
| illegal :- instance\_of(X,person) & age(X,Y) & min(0,Y,Y)         |
| illegal :- instance\_of(X,person) & age(X,Y)& min(100,Y,100)      |

#### 3.1.7 Inheritance - Kế thừa

Những giá trị quan hệ của một lớp được cho là kế thừa từ những thể hiện của nó. Ví dụ như, nếu chúng ta khẳng định rằng art là một thể hiện của lớp brown\_haired\_person, chúng ta có thể kết luận has\_hair\_color(art,brown). Nói chung, một đối tượng có thể là thể hiện của nhiều lớp. Trong trường hợp đa kế thừa, những giá trị kế thừa được từ những lớp khác nhau có thể xung đột và gây ra vi phạm ràng buộc, Ví dụ, nếu art là một thể hiện của lớp brown\_haired\_person, và một lớp bald\_person với ràng buộc là người đó không có tóc, chúng ta sẽ mắc phải vi phạm ràng buộc. Trong trường hợp vi phạm ràng buộc, hoặc là giá trị vị phạm ràng buộc phải được loại bỏ hoặc những kỹ thuật lý luận không nhất quán (para-consistent reasoning) phải dược sử dụng để xử lý những trường hợp không nhất quán như vậy.

#### 3.1.8 Reasoning with Classes - Suy luận với các lớp

Có bốn loại suy luận được quan tâm với các lớp:

\- (1) Cho hai lớp A và B, liệu A có phải là lớp con của B?

\- (2) Cho một lớp A và một thể hiện I, liệu I có là một thể hiện của A?

\- (3) Cho một quan hệ xác định nó là đúng hay sai?

\- (4) Cho một quan hệ, xác định những những giá trị của các biến làm cho nó đúng.

Hai suy luận đầu tiên tương đương với việc tính toán trên quan điểm quan hệ subclass và instance\_of. Chúng cũng có thể được cài đặt bằng các thuật toán tìm kiếm đường đi trên đồ thị xác định bởi các lớp và các thể hiện của chúng. Hai suy luận cuối tương đương với quan đỉểm quan hệ nhỏ được quan tâm.

### 3.2 Rule-based Reasoning - Suy luận dựa trên luật

Không có ranh giới rõ ràng giữa rule-based reasoning và taxonomic reasoning. Cho dù chúng ta sử dụng thông qua Datalog như một ngôn ngữ đặc tả cho taxonomic reasoning. Nó có thể cài đặt rất nhiều những suy luận mong muốn trong một rule engine. Trong phần này, chúng ta sẽ xem xét một ví dụ về rule-based reasoning mà liên quan tới dạng nâng cao của những luật được gọi là quy luật tồn tại. Chúng ta sẽ bắt đầu với một ví dụ đồ thị tri thức mà cận những suy luận như vậy và sau đó chúng ta sẽ đề cập những thuật toán suy luận dựa trên luật (rule-based reasoning algorithm) thực hiện những suy luận được yêu cầu.

#### 3.2.1 Example Scenario Requiring Rule-based Reasoning - Ví dụ về trường hợp cần suy luận dựa trên luật

Xem xét một đồ thị thuộc tính với lược đồ được cho ở bên dưới đây. Những công ti sản suất sản phẩm chứa hoá chất. Những người có liên quan tới nghiên cứu hoá học và họ có thể được tài trợ bởi những công ty.

![]({{ site.url }}{{ site.baseurl }}/assets/img/2021-06-28-what-are-some-inference-algorithms/media/image1.png)Cho đồ thị thuộc tính như trên, chúng ta quan tâm đến việc quyết định xem nếu một người có thể có xung đột lợi ích khi tham gia vào một nghiên cứu. Chúng ta có thể định nghĩa quan hệ xung đồ bằng cách sử dụng luật Datalog sau đây:

|                                                                                     |
| ----------------------------------------------------------------------------------- |
| coi(X,Y,Z) :- involved\_in(X,Y) & about(Y,P) & funded\_by(X,Z) & has\_interest(Y,P) |
| has\_interest(X,Z) :- produces(X,Y) & contains(Y,Z)                                 |

Quan hệ has\_interest không phải nằm trong lược đồ đồ thị thuộc tính được thêm vào. Nhưng với sự giúp đỡ của việc định nghĩa nó bằng cách dùng một luật, một rule engine có thể tính toán xung đột của quan hệ quan tâm đến coi. Trong một vài trường hợp, chúng ta có thể quan đến việc thêm vào những giá trị đã được tính toán của quan hệ coi vào đồ thị tri thức của chúng ta. Vì coi là quan hệ ba ngôi, chúng ta sẽ cần phải tái tổ chức nó. Vì tái tổ chức yêu cầu thêm vào những đối tượng mới trong đồ thị, chúng ta có thể xác định chúng bằng cách sử dụng một quy luật tồn tại được cho bên dưới:

|                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------- |
| ∃c conflict\_of(c,X) & conflict\_reason(c,Y) & conflict\_with(c,Z) :- involved\_in(X,Y) & about(Y,P) & funded\_by(X,Z) & has\_interest(Y,P) |

Nói chung, những luật tồn tại cần thiết bất cứ khi nào chúng ta cần phải tạo ra những đối tượng mới trong đồ thị tri thức. Tái tổ chức quan hệ là một tình huống cụ thể. Đôi khi, chúng ta có thể cần tạo ra những đối tượng mới thoã mãn những ràng buộc xác dịnh (certain constraints). Ví dụ như, xem xét một ràng buộc: mọi con người phải có hai cha me. Với một người, cha mẹ có thể không cần biết, và nếu chúng ta muốn đồ thị tri thức của chúng ta tiếp tục phù hợp với ràng buộc này, chúng ta phải thêm vào hai đối tượng biểu diễn cha me như một người. Vì điều này có thể dẫn đến vô số các đối tượng mới, nên điển hình là đặt giới hạn về cách các đối tượng mới được tạo ra.

#### 3.2.2 Approach for Rule-based Reasoning - Phương pháp tiếp cận cho suy diễn dựa trên luật

Để hỗ trợ suy luận dựa trên luật trên đồ thị tri thức, chúng ta thường dùng một rule engine với dữ liệu trên đồ thị tri thức. Chúng ta đề cập ở đây một vài chiến lược suy luận khác nhau được sử dụng bởi những rule engine.

Trong chiến lược bottom-up, được gọi là Chase, chúng ta áp dụng tất cả những luật dựa trên đồ thị tri thức, và thêm vào một số dữ kiện mới cho nó cho đến khi chúng ta không cần phải khai báo những dữ kiện mới nữa. Như đã nói đến ở phần trước, chúng ta cần đưa ra những chiến lược dừng để đối phó với những tình huống mà những suy luật thêm vào không cung cấp những thông tin hữu ích. Khi chúng ta tính toán xong Chase, suy luận có thể được thực hiện bằng những phương thức truy vấn truyền thống.

Trong xử lý truy vấn top-down, chúng ta bắt đầu từ câu truy vấn sẽ được trả lời, và áp dụng những luật cơ bản nhất. Một chiến lược top-down cần một tương tác chặt chẽ giữa engine truy vấn của đồ thị tri thức với luật đánh giá. Với tiếp cận này, cách tiếp cận này có thể sử dụng ít không gian hơn rất nhiều so với chiến lược lập luận bottom-up

Những luật engine có độ hiệu quả cao và có thể mở rộng sử dụng những truy vấn tối ưu (query optimization) và những kỹ thuật ghi lại (rewriting techniques). Chúng cũng dựa trên việc nắm bắt các chiến lược để đạt được hiệu quả thực thi.

## 4\. Tổng kết

Trong chương này, chúng ta đã đề cập những thuật toán suy diễn khác nhau cho đồ thị tri thức. Những thuật toán đồ thị như tìm kiếm đường đi, xác định công đồng, … được hỗ trợ bởi hầu hết các graph engine trong thực tế. Graph engine thường giới hạn hỗ trợ cho ontology và rule-based reasoning. Các engine đồ thị tri thức (Knowledge Graph Engines) hiện đang bắt đầu trở nên sẵn sàng hỗ trợ cả các thuật toán đồ thị tổng quát cũng như ontology và rule-based reasoning

**Bài tập:**

...Sẽ cập nhật sau…

Bài giảng gốc: https://web.stanford.edu/class/cs520/2020/notes/What\_Are\_Some\_Inference\_Algorithms.html
