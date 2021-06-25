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

**HOW TO CREATE A KNOWLEDGE GRAPH?**

**1. Giới thiệu**

Ta có thể bắt đầu với đồ thị tri thức mà không cần thiết kế trước lược đồ (schema) của nó và phát triển cả lược đồ (schema) lẫn các thể hiện (instances) của nó trong suốt quá trình xử lý. Ở mức độ một bản thiết kế trước lược đồ đồ thị tri thức trong thực tế, nó có thể cải thiện đáng kể tính hữu dụng của nó. Giống như một thiết kế liên quan đến việc đưa ra một lựa chọn hợp lý những node, nhãn nút, những thuộc tính node, những quan hệ và những thuộc tính quan hệ.

Đầu vào cho quần thể đồ thị tri thức có thể đến từ một hoặc nhiều nguồn bao gồm dữ liệu có cấu trúc (structured data), dữ liệu bán cấu trúc (semi structured data), văn bản (free text) hoặc hình ảnh (images) hoặc được nhập trực tiếp bởi con người (direct authoring by human input). Khi chúng ta đang làm việc với nguồn dữ liệu có cấu trúc (structured data) và dữ liệu bán cấu trúc (semi structured data), chúng phải thực hiện tác vụ ánh xạ lược đồ (schema mapping task) (tức là, liên hệ lược đồ trong nguồn dữ liệu đầu vào với lược đồ của đồ thị tri thức) và tác vụ ghi liên kết (record linkage task) (tức là liên hệ những thể hiện mới với những thể hiện đã tồn tại từ trước trong đồ thị tri thức). Những những tác vụ cũng đối mặt trong suốt quá trình tích hợp dữ liệu (data integration) với chỉ một khác biệt là dữ liệu tích hợp được thể hiện trong mô hình dữ liệu đồ thị. Khi chúng ta đang làm việc với nguồn dữ liệu phi cấu trúc (unstructured sources), chúng ta phải giải quyết vấn đề rút trích thông tin trong tác vụ rút trích thực thể (entity extraction) và rút trích quan hệ (relation extraction)

Sự lựa chọn phương pháp sử dụng trong quần thể đồ thị tri thức phụ thuộc vào quy mô của vấn đề và độ chính xác mong muốn. Nếu một đồ thị tri thức được sử dụng trên quy mô web cho truy xuất thông tin (information retrieval), độ chính xác không cần phải hoàn hảo, và không sử dụng định danh con người cho mọi bộ ba của đồ thị. Nếu một đồ thị tri thức được sử dụng trong doanh nghiệp, nơi mà độ chính cần phải càng chính xác càng tốt (tiệm cần hoàn hảo), định danh con người là cần thiết ngay cả khi nó được thực hiện ngay trước khi thông tin được sử dụng. Độ chính xác luôn được mong muốn bất kể là doanh nghiệp hay cài đặt WW, để đảm bảo hiệu quả chi phí (cost effectiveness) và khả năng mở rộng (scalability), phải chú trọng đến nguồn cung cấp từ cộng đồng và các phương pháp giảm thiểu chi phí trong việc lấy thông đầu vào từ con người

**2. Thiết kế đồ thị tri thức**

Cả đồ thị thuộc tính (Property Graph) và mô hình dữ liệu RDF (RDF Data Model) có một tập các vấn đề thiết kế, một vài trong số đó thường gặp ở cả hai, trong khi số khác thì chỉ cần ở một loại duy nhất.

Lấy ví dụ, cả hai mô hình đều cần phải sử dụng tái tổ chức cho những tình huống không thể mô hình hoá trực tiếp bằng cách sử dụng bộ ba. Một mô hình RDF (RDF Model) cần phải áp dụng một lược đồ cho IRIs điều mà không cần thiết với đồ thị thuộc tính (Property Graphs). Trong mô hình đồ thị thuộc tính (Property Graph Model), chúng ta cần phải quyết liệu rằng một giá trị có nên được biểu diễn như một thuộc tính (property) hay như một nút (node), trong khi sự phân biệt này không cần thiết trong một mô hình RDF. Trong phần này, chúng ta sẽ tìm hiểu tổng quan một số vấn đề thiết kế gặp phải với hai mô hình này.

**2.1 Thiết kế một RDF Graph - Design of an an RDF Graph**

Các nguyên tắc tạo biểu đồ tri thức cho dữ liệu RDF trên WWW được gọi là các nguyên tắc dữ liệu được liên kết - linked data principles như sau:

\- Sử dụng URIs như tên gọi cho mọi thứ

\- Sử dụng HTTP URIs nên mọi người có thể tra cứu những tên gọi này

\- Khi một người nào đó tra cứu một URI, cung cấp những thông tin hữu ích, sử dụng các chuẩn (RDF, SPARQL)

\- Bao gồm liên kết đến những URIs khác, nên họ có thể khám phá nhiều thứ hơn

**2.1.1 Sử dụng URI như định danh cho các sự vật**

Để xuất bản một đồ thị tri thức lên WWW, đầu tiên chúng ta phải định danh những thành phần quan tâm trong miền của chúng ta. Chúng là những thứ mà những thuộc tính và quan hệ của chúng, chúng ta muốn mô tả trên đồ thị. Trong thuật ngữ WWW (WWW terminology), tất cả nhưng thành phần quan tâm ấy được gọi là tài nguyên – resources. Những tài nguyên có hai loại: tài nguyên thông tin (information resources) và tài nguyên phi thông tin (non-information resources). Tất cả những tài nguyên mà chúng ta tìm kiếm trên WWW truyền thống như tài liệu (documents), hình ảnh (images) và những tập tin phương tiện (media files) là những tài nguyên thông tin (information resources) . Nhưng nhiều thứ chúng ta muốn trong đồ thi tri thức không phải con người (People), sản phẩm vật lý (physical product), nơi chốn (places), proteins, những khái niệm khoa học (scienctific concepts), …. Như một quy luật chung, tất cả “những thực thể thế giới thực” mà tồn tại bên ngoài WWW đều là tài nguyên phi thông tin (non-information resources)

Những người xuất bản đồ thị tri thức nên xây dựng URI để chia sẻ theo một cách đơn giản, ổn định và dễ quản lý. Nói gọn hơn, URI dễ nhớ sẽ không dễ bị hư hại khi được gửi trong email và nói chung dễ nhớ hơn :v Sau khi chúng ta cài đặt một URL để định danh một tài nguyên xác định, nó sẽ duy trì càng lâu càng tốt. Để đảm bảo tính bền bỉ lâu dài, tốt nhất là giữ các bit và phần cụ thể về triển khai, chẳng hạn như “.php”, và “.asp” ra ngoài URIs. Cuối cùng, URI nên được định nghĩa theo cách mà chúng có thể được quản lý bởi những người xuất bản (Developer chẳng hạn)

**2.1.2 Sử dụng HTTP URIs để mà con người có thể tra cứu chúng**

Chúng ta định danh những tài nguyên bằng cách sử dụng Uniform Resources Identifiers (URIs) - Bộ định danh tài nguyên nguyên đồng nhất. Chúng ta tự hạn chế chỉ sử dụng các URI HTTP và tránh các lược đồ URI khác như Uniform Resource Names (URN) và Digital Object Identifiers (DOI).

Quá trình xử lý của việc tra cứu tên gọi là tham chiếu URI - URI dereferencing. Khi chúng ta tham chiếu một URI cho một đối tượng thông tin, chúng ta mong đợi có được biểu diễn trạng thái hiện tại của nó (ví dụ như là một tài liệu văn bản, một hình ảnh, một video, …) Nhưng khi chúng ta tham chiếu một tài nguyên phi thông tin, chúng ta có thể nhận được mô tả trong biểu diễn RDF trong một định nghĩa XML

**2.1.3 Khi một ai đó tra cứu một URI, cung cấp những thông tin hữu ích sử dụng RDF và SPARQL**

Khi một ai đó tra cứu một URI, nhà cung cấp nên trả về một đồ thị tri thức trong RDF. Dữ liệu nên tái sử dụng những từ vựng được chuẩn hoá để đặt tên những IRIs được sử dụng trong mô tả dữ liệu RDF. Những từ vựng hữu ích có sẵn cho việc mô tả dữ liệu danh mục, những tổ chức và dữ liệu đa chiều (multidimensional data), như là thống kê trên Web. Một nổ sự mã nguồn mở gọi là Schema.Org công bố bởi cộng đồng từ vựng mã nguồn mở cho việc sử dụng trên khắp Web. Chúng ta xem xét một vài ví dụ về những từ vựng đấy

Dữ liệu RDF sau đây mô tả một đoạn về cơ cấu tổ chức của Văn phòng Nội các Vương quốc Anh.

@prefix uk\_cabinet: \<http://reference.data.gov.uk/id/department/\>

uk\_cabinet:co rdf:type org:Organization

uk\_cabinet:co skos:prefLabel "Cabinet Office"

uk\_cabinet:co org:hasUnit uk\_cabinet:cabinet-office-communications

uk\_cabinet:cabinet-office-communications rdf:type org:OrganizationUnit

uk\_cabinet:cabinet-office-communications skos:prefLabel "Cabinet Office Communications"

uk\_cabinet:cabinet-office-communications org:hasPost uk\_cabinet:post\_246

uk\_cabinet:post\_246 skos:prefLabel "Deputy Director, Deputy Prime Minister's Spokesperson"

Dữ liệu phía trên, bộ ba đầu tiên sử dụng lớp org:Organization từ Organization Ontology.

Bộ ba thứ hai sử dụng quan hệ skos:prefLabel được vẽ từ SKOS ontology. SKOS chuẩn hoá cho một Simple Knowledge Organization System, và cung cấp một vài quan hệ chung hữu ích như skos:prefLabel cho việc mô tả dữ liệu. Trong trường hợp này, skos:prefLabel đơn giản cho phép chúng ta liên hệ một nhãn văn bản uk\_cabinet:co.

Bộ ba thứ ba sử dụng quan hệ org:hasUnit từ Organization ontology một tả một đơn vị trong UK Cabinet office

Hai bộ ba tiếp theo bổ sung khẳng định về đơn vị này

Bộ ba thứ sáu sử dụng quan eh65 org:hasPost mô tả vị trị với một phòng ban (department)

Và hai bộ ba cuối cùng cho thông tin bổ sung về vị trị đó

Không phải lúc nào cũng có thể tìm thấy những từ vựng tồn tại trước đó có thể được sử dụng trong khởi tạo RDF dataset. Nếu việc khởi tạo mới một từ vựng trở nên cần thiết, chúng ta nên đảm bảo rằng nó được ghi lại, tự mô tả, có chính sách phiên bản, được định nghĩa trong nhiều ngôn ngữ, và được xuất bản bởi một nguồn đáng tin cậy để mà các tồn tại URIs sử dụng nó trong một khoảng thời gian dài. Chúng ta nói rằng một từ vựng tự mô tả nếu mỗi thuộc tính hoặc thuật ngữ có một nhãn, khái niệm và chú thích được định nghĩa.

**2.1.4 Bao gồm các tới các URIs khác, nên họ có thể khám phá nhiều thứ hơn**

Trong khi xuất bản dữ liệu bằng cách sử dụng RDF, chúng ta nên cung cấp liên kết đến những đối tượng để mà tăng tính hữu ích của nó. Có 3 loại liên kết:

\- Relationship links - liên kết quan hệ

\- Identity links - liên kết thực thể

\- Vocabulary links - liên kết từ vựng

Liên kết quan hệ (Relationship links) trỏ đến những thứ liên hệ trong những nguồn dữ liệu khác như những người khác, những nơi chỗ hoặc genes. Ví dụ, liên kết quan hệ cho phép con người có thể có trỏ đến những thông tin lai lịch về nơi mà họ sinh sống, hoặc dữ liệu thư mục về những công bố mà họ đã viết. Trong bộ ba sau đây, chúng ta thấy một liên kết mà một cá nhân trong một tập dữ liệu đươc xác nhận là sống gần một vị trí địa lý được chỉ định bằng cách sử dụng URI trong một tập dữ liệu khác.

@prefix big: \<http://biglynx.co.uk/people/\>

@prefix dbpedia: \<http://dbpedia.org/resource/\>

big:dave-smith foaf:based\_near dbpedia:Birmingham

Liên kết thực thể (Identity links) trỏ đến những URI bí danh sử dụng bởi những nguồn dữ liệu khác để định danh cùng một đối tượng trong thế giới thực hoặc khái niệm trừu tượng, Liên kết thưc thể cho phép khách hàng (clients) có thể truy xuất nhiều mô tả về một thực thể và phục vụ một chức năng xã hội quan trọng vì chúng cho phép nhiều góc nhìn khác nhau về thế giới được thể hiện trên WWW. Nó là một chuẩn thực thể để sử dụng loại liên kết <http://www.w3.org/2002/07/owl#sameAs> để thông báo hai bí danh URI cùng tham chiếu đến cùng một nguồn.

Lấy ví dụ, nếu Dave Smith cùng muốn bảo trì một dữ liệu trang chủ ẩn danh bên cạnh dữ liệu mà Big Lynx công khai về anh ta, anh có thể thêm một liên kết <http://www.w3.org/2002/07/owl#sameAs> đến dữ liệu trang chủ ẩn danh, việc thông báo URI sử dụng tham chiếu đến tài liệu và URI sử dung bởi Lynx cùng tham chiếu đến cùng một thưc thể thế giới thực. Một bộ ba biểu diễn thông tin như thế được mô tả sau đây:

@prefix ds: \<http://www.dave-smith.eg.uk\>

@prefix owl: \<http://www.w3.org/2002/07/owl\>

@prefix big: \<http://biglynx.co.uk/people/\>

ds:me owl:sameAs big:dave-smith

Liên kết từ vựng trỏ trừ dữ liệu đến những định nghĩa của những thuật ngữ từ vựng được sử dụng để biểu diễn dữ liệu, giống như từ những định nghĩa này đến những định nghĩa của những thuật ngữ được liên hệt trong những từ vựng khác. Liên kết từ vựng làm cho dữ liệu tự mô tả và cho phép ứng dụng liên kết dữ liệu (Link Data) hiểu và tích hợp dữ liệu thông quan những từ vựng. Trong liên kết từ vựng được cho sau đây, lớp SmallMediumEnterprise định nghĩa bởi BigLynx được định nghĩa thành một lớp con của lớp Company trong DBpedia Ontolgy. Bằng cách tạo ra một liên kết như thế, có thể truy xuất các xác nhận khác nhau về lớp Company từ DBPedia, và sử dụng chung với lớp SmallMediumEnterprise.

@prefix dbpedia: \<http://dbpedia.org/ontology/\>

big:sme\#SmallMediumEnterprise rdfs:subClassOf dbpedia:Company

**2.2 Thiết kế một đồ thị thuộc tính (Property Graph)**

Thiết kế một đồ thị thuộc tính liên quan đến chọn nút (nodes), nhãn nút (node labels), thuộc tính nút (node properties), cạnh liên kết (edges) và thuộc tính cạnh liên kết (edge properties). Những câu hỏi thiết kế cơ bản là liệu có nên mô hình hoá một phần thông tin như một thuộc tính, nhãn hay như một đối tượng riêng biệt; khi nào nên đưa vào những thuộc tính quan hệ; và làm thế nào có thể xử lý những mối quan hệ đặc biệt (higher arity relationships). Chúng ta sẽ minh họa quá trình thực hiện những lựa chọn này bằng cách sử dụng các ví dụ.

**2.2.1 Lựa chọn nút (Nodes), nhãn (Labels) và thuộc tính (Properties)**

Trong một mô hình đồ thị thuộc tính, những nút thường biểu diễn những thực thể trong miền, Nếu chúng dược biểu diễn với thông tin biểu diễn về con người, chúng ta sẽ khởi tạo một nút cho mỗi cá nhân (ví dụ John), và liên hệ nhãn Person với nút đó.

Có nhiều cân nhắc trong tạo ra nhiều lựa chọn hơn những nhãn nút, những thuộc tính nút và cạnh liên kết. Những cân nhắc này bao gồm: tính tự nhiên của nhãn, liệu các nhãn có thể thay đổi trong một khoảng thời gian, hiệu suất truy vấn thời gian chạy và số lượng các giá trị

Để minh hoạ sự lựa chọn liệu có nên mô hình hoá một phần thông tin thành một nhãn, thuộc tính hay thành một đối tượng riêng biệt, xem xét tác vụ biểu diễn giới tính của một người. Chúng ta có ba cách tìm năng để biểu diễn thông tin này:

\- (1) Chúng ta có thể khởi tạo :Male và :Female như những nhãn và liên hệ chung với những nút Person

\- (2) Chúng ta có thể khởi tạo một thuộc tính gọi là “Gender” và liên hệ nó với nút Person và cho phép nó có thể có giá trị “male” và “female”

\- (3) Chúng ta có thể khởi tạo đối tượng Gender, liên hệ nó với Person bằng cách sử dụng mối quan hệ has\_gender, và cho nó một thuộc tính gọi là “name” mà có thể lấy “male” và “female” như những giá trị của nó

Những nhãn trong một mô hình đồ thị thuộc tính được sử dụng để nhóm những nút thành những tập hợp. Tất cả những nút được gán nhãn với cùng nhãn sẽ thuộc về cùng một tập. Những truy vấn có thể hoạt động với những tập hợp thay vì toàn bộ đồ thị, tạo ra những câu truy vấn dễ dàng hơn, và hiệu quả hơn. Một nút có thể được gán nhãn với bất kỳ nhãn nào, kể cả rỗng, việc tạo nhãn là một tuỳ chọn bổ sung cho đồ thị. Như nhóm những nhãn nút thành một tập, nó có thể được nhìn như một lớp. Câu hỏi đặt ra là liệu có thể đưa một nhãn mới có thể được đặt lại như đưa vào một lớp mới hay không?

Khởi tạo những lớp mới Male và Female so với đưa vào một thuộc tính nút “gender” mà có thể nhận giá trị “male” và “female” biểu diễn cùng một thông tin. Một cách tổng quát, bất cứ khi nào một cụm từ xuất hiện một cách tự nhiên trong ngôn ngữ một cách thường xuyên được sử dụng trong một miền, nó là một ứng viên có thể được thêm vào như một lớp miễn là số lượng thành viên trong lớp không thay đổi theo thời gian. Như một số cài đặt tối ưu truy xuất dựa trên sử dụng nhãn, việc sử dụng nhãn có thể cho kết quả truy vấn với hiệu suất cao mà cần thiết để lọc những kết quả dựa trên thành viên trong lớp. Nếu lớp các thành viên thay đổi theo thời gian, cả nhãn hay giá trị thuộc tính nút đều không phải là lựa chọn thích hợp, chúng ta cần phải sử dụng một mối quan hệ. Chúng ta sẽ xem xét vấn đề này trong phần dưới đây :v

**2.2.2 Khi đưa vào mối quan hệ (Relationships) giữa những đối tượng (Objects)**

Với những tình huống có thể mô hình hoá thay vì sử một thuộc tính nút hoặc đưa vào một đối tượng riêng biệt và mối quan hệ, ở đây, ít nhất, có hai cân nhắc khác nhau. Cân nhắc đầu tiên được giới thiệu trong phân phía trên: những thành viên trong lớp thay đổi theo thời gian. Cân nhắc thứ hai phát sinh khi chúng ta mong muốn đạt đươc hiệu năng tốt hơn. Chúng ta sẽ xem xét những tình huống này chi tiết hơn

Tiếp tục với ví dụ từ phần trước, khi giới tính của một người có thể thay đổi trong một khoảng thời gian, do đó lựa chọn của chúng ta chỉ có thể là biểu diễn thông tin như một đối tượng Gender riêng biệt mà có thể liên hệ với Person bằng cách sử dụng quan hệ has\_gender. Chúng ta có thể liên hệ một mối quan hệ thuộc tính với mối quan hệ has\_gender mà cho biết khoảng thời gian mà giá trị cụ thể của giới tính đó nắm giữ. Khởi tạo một nút riêng biệt Gender, tuy nhiên sẽ dẫn tới một số lượng lớn các cạnh liên kết gây lãng phí vì hầu hết mọi người thì giới tính không đổi. Trong trường hợp như thế, có thể mong muốn một kết hợp hai giải pháp trong đó, đối với hầu hết mọi người, giới tính được biểu diễn như một giá trị thuộc tính nút, nhưng với một số ít người, nó được biểu diễn như một giá trị quan hệ thuộc tính đến một nút Gender riêng biệt.

Chúng ta xem xét một tình huống mà việc truy vấn hiệu suất tốt hơn là một yếu tố quan trọng cần cân nhắc. Giả định rằng, chúng ta mong muốn mô hình hoá những bộ phim và những thể loại của chúng. Trong một thiết kế, với một nút thuộc kiểu Movie, chúng ta có thể thêm một thuộc tính “genre” mà có thể nhận những giá trị như “Action”, “SciFci”, … Trong một thiết kế khác, chúng ta có thể thêm một nút kiểu Genre mà có một thuộc tính nút là “name” mà có thể nhận những giá trị như là “Action”, “SciFci”. Sau đó chúng ta sẽ liên hệ một nút kiểu Movie với một nút kiểu Genre bằng cách sử dụng mối quan hệ has\_genre. Tổng quát, chúng ta có thể liên kết nhiều hơn một thể loại với một bộ phim. Giả định rằng chúng ta mong muốn truy vấn những bộ phim mà có ít nhất một thể loại chung. Giải pháp đầu tiên là chúng ta sử dụng một thuộc tính nút “genre”, trong truy vấn này sẽ được viết bằng Cypher:

MATCH (m1:Movie), (m2:Movie)

WHERE any(x IN m1.genre WHERE x IN m2.genre)

AND m1 \<\> m2

RETURN m1, m2

Khi chúng ta mô hình hoá thể loại như một đối tượng riêng biệt, truy vấn tương tự cũng tự viết như sau:

MATCH (m1:Movie)-\[:has\_genre\]-\>(g:Genre),

(m2:Movie)-\[:has\_genre\]-\>(g)

WHERE m1 \<\> m2

RETURN m1, m2

Trong truy vấn thứ hai ở trên, chúng ta có khả năng sử dụng một cách trực tiếp mẫu đồ thị (graph patterns) và trong một số graph engine, truy vấn này có một hiệu suất thời gian chạy nhanh hơn (faster runtime performance) bởi vì lập chỉ mục trên các mối quan hệ.

Do đó, trong trường hợp này, người ta phải chọn giữa hai thiết kế tùy thuộc vào loại truy vấn sẽ được mong đợi.

**2.2.3 Khi đưa vào mối quan hệ (Relationships) giữa những thuộc tính (Properties)**

Chúng ta đã thấy một ví dụ về một thuộc tính liên hệ với một mối quan hệ để giải quyết tình huống khi mối quan hệ thay đổi theo thời gian. Những tình huống khác mà chúng có ý nghĩa để thêm những thuộc tính với mối quan hệ bao gồm liên hệ trọng số hoặc độ tin cậy với một mối quan hệ hoặc liên hệ nguồn gốc hoặc meta data khác với mối quan hệ

Một số grah engine không chỉ mục dựa trên những mối quan hệ thuộc tính. Nếu sử dụng trường hợp như vậy mà một lượng lớn đánh giá truy vấn có thể hoàn thành mà không cần sử dụng những mối quan hệ thuộc tính, và chúng chỉ cần cho lọc kết quả cưới cùng, chúng ta không cần phải trả giá về mặt hiệu năng vì thiếu chỉ mục. Nếu truy cập đến những quan hệ thuộc tính là trọng tâm của hiệu suất truy vấn, tốt hơn nó nên được sửa đổi quan hệ, và chúng ta sẽ thảo luận ngay phần bên dưới :v

**2.2.4 Xử lý các mối quan hệ phi nhị phân (Handling non-binary Relationships)**

Chúng ta thường xuyên cần phải mô hình hoá những mối quan hệ mà không phải nhị phân. Một ví dụ chung về một mối quan hệ như là mối quan hệ between được cho bởi những đối tượng A, B và C mà C là between A và B. Một tiếp cận chuẩn để biểu diễn những mối quan hệ đặc biệt cao này trong một đồ thị là tái tổ chức (reification). Chúng ta đã thảo luận trước đó về tái tổ chức (reification) trong một ngữ cảnh của RDF, nhưng kỹ thuật này cũng hữu ích và đáng kỳ vọng như nhau đối với đồ thị. Để nắm bắt mối quan hệ between, chúng ta thể vào một nút kiểu Between\_Relationship mà có hai thuộc tính: bas\_object (với những giá trị là A và B) và has\_between\_object (với giá trị C). Chúng ta có thể sử dụng tái tổ chức cho những quan hệ với bất kỳ đặc biệt nào bằng cách khởi tạo một nút kiểu mới cho quan hệ, và bằng cách thêm những thuộc tính nút cho những tham số khác nhau của quan hệ đó.

**3. Tổng kết**

**Bài tập:**

...Sẽ cập nhật sau…

**Bài giảng gốc: https://web.stanford.edu/class/cs520/2020/notes/How\_To\_Create\_A\_Knowledge\_Graph.html**
