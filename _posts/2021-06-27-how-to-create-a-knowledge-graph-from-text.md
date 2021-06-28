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

# HOW TO CREATE A KNOWLEDGE GRAPH FROM TEXT

**LÀM THẾ NÀO KHỞI TẠO MỘT ĐỒ THI TRI THỨC TỪ VĂN BẢN**

## 1\. Giới thiệu

Những nguồn dữ liệu văn bản giống như tin tức kinh doanh và tài chính, những hồ sơ SEC, và những trang web như Wall Street Journal, chứa thông tin có giá trị cao cho những tác vụ kinh doanh như nghiên cứu thị trường - market research, kinh doanh thông minh - business intelligence, … Chúng ta có thể sử dụng Xử lý ngôn ngữ tự nhiên (Natural Language Processing -NLP) để xử lý những nguồn dữ liệu, và khởi tạo đồ thị tri thức để có thể hỗ trợ nhiều loại phân tích. Tuy nhiên, NLP là một công nghệ chuyên biệt (specialized) và rất phức tạp (sophisticated) và mục đích của chúng ta không phải cung cấp một phạm vi toàn diện và chi tiết về nó. Mục đích của chúng ta ở đây là dựa vào những khái niệm cơ sở của NLP mà có thể hữu ích trong nhiều mối quan tâm chính và mục tiêu chính vẫn là khởi tạo một đồ thị tri thức. Một số nhà cung cấp đã tạo ra các dịch vụ kinh doanh xoay quanh việc xử lý văn bản ngôn ngữ tự nhiên và cung cấp dữ liệu có cấu trúc cho những người khác để tiêu thụ.

Có ba tác vụ Xử lý ngôn ngữ tự nhiên - NLP task liên hệ trực tiếp đến xây dựng đồ thị tri thức (knowledge graph construction):

\- (1) Entity Extraction - Rút trích thực thể

\- (2) Relation Extraction - Rút trích quan hệ

\- (3) Entity Resolution - Phân giải thực thể

Entity Extraction - Rút trích thực thể là tác vụ định danh những thực thể chính (key entities) được quan tâm (ví dụ: Organizations - Tổ chức, People - Con người, Place - Nơi chốn, …) từ văn bản. Những thực thể này thông thường tạo nên nút (node) trong một đồ thị tri thức.

Relation Extraction - Rút trích quan hệ là tác vụ mà khi được cho hai thực thể quan tâm, và một số văn bản, chúng rút trích ra những quan hệ giữa chúng (ví dụ: net sales, management team information, … ) từ văn bản. Thỉnh thoảng, rút trích quan hệ cũng được dùng để rút trích những thuộc tính của một thực thể được cho trước. Mối quan hệ và những thuộc tính được rút trích thông thường sẽ trở thành những mối quan hệ hoặc những thuộc tính nút trong đồ thị tri thức của chúng ta.

Entity Resolution - Phân giải thực thể là tác vụ định danh xem nhiều đề cập trong một văn bản có tham chiếu đến cùng một thực thể hay không. Ví dụ như, trong một đoạn văn bản, “John Smith”, “He” và “Her father” có thể tất cả cùng tham chiếu đến cùng một thực thể.

Trong chương này, chúng ta sẽ tìm hiểu một cái nhìn tổng quan về những kỹ thuật được sử dụng trong rút trích thực thể (Entity Extraction ) và quan hệ (Relation Extraction). Chúng ta sẽ không thảo luận về phân giải thực thể - entity resolution trong phần thảo luận này bởi vì nó là một đề tài nâng cao so với phạm vi trình bày hiện tại :)) Hầu hết những kỹ thuật cho rút trích thực thể và quan hệ, mà phổ biến hiện nay, dựa trên điều chỉnh với một mô hình ngôn ngữ được huấn luyện từ trước (pre-trained language model) trong tác vụ đang được thực hiện. Với mục đích của chúng ta, chúng ta coi những mô hình ngôn ngữ được huấn luyện từ trước (pre-trained language model) và những kỹ thuật máy học (machine learning techniques) như những chiếc hộp đen có sẵn để sử dụng như những món hàng bán sẵn ngoài chợ (off-the-shelf commodities). Quá trình này trong Xử lý ngôn ngữ tự nhiên - NLP và Máy học - Machine Learning cho phép những người tạo ra đồ thị tri thức tập trung vào sản phẩm cuối cùng, và cung cấp những dữ liệu huấn luyện và đánh giá thích hợp mà cần thiết cho sự điều chỉnh của mô hình ngôn ngữ (language models). Chúng ta sẽ bắt đầu với một tổng quan về mô hình ngôn ngữ và sao đó mô tả chi tiết các tác vụ rút trích thực thể và rút trích quan hệ.

## 2\. Tổng quan về mô hình ngôn ngữ - Overview of Language Models

Mô hình ngôn ngữ là tác vụ dự đoán xem từ nào xuất hiện kế tiếp trong một văn bản. Ví dụ, cho một câu: “students opened their”, một mô hình ngôn ngữ sẽ dự đoán từ kế tiếp mà có thể hoàn thành câu này. Trong trường hợp này, từ kế tiếp có thể là book, exam, laptop, …

Tổng quát hơn, cho một tập hợp những từ $x\_1, x\_2, …, x\_{n-1}$, một mô hình ngôn ngữ dự đoán xác suất $P(x\_n \\|\\ x\_1, x\_2, …, x\_{n-1})$, trong đó $x\_n$ là một từ bất kỳ trong bộ từ vựng. Mô hình ngôn ngữ có thể được sử dụng rỗng rãi trong tự động hoàn thành yêu cầu tìm kiếm trên web, trong tự động chỉnh sửa từ trong xử lý từ, …

Mô hình ngôn ngữ hiện đại được tạo ra bằng cách huấn luyện một mô hình Học sâu (Deep Learning Model), như là Recurring Neural Network, trên một kho ngữ liệu văn bản cực lớn. Nhiều biến thể của các mô hình ngôn ngữ được huấn luyện trướccó sẵn như những sản phẩm mã nguồn mở có thể được tinh chỉnh cho mục đính của những tác vụ xác định đang thực hiện. Vì chúng ta đang thảo luận những kỹ thuật cho rút trích thực thể và rút trích quan hệ, chúng ta cũng sẽ mô tả làm thế nào mà mô hình ngôn ngữ có thể được tinh chỉnh cho những tác vụ này.

## 3\. Rút trích thực thể - Entity Extraction

Chúng ta sẽ bắt đầu bằng cách xem xét một ví dụ cụ thể về rút trích thực thể và sau đó tìm hiểu tổng quan những cách tiếp cận khác nhau cho rút trích thực thể và kết lại phần này bằng thảo luận về một số thách thức trong việc thực hiện tốt ở tác vụ này.

### 3.1 Ví dụ về rút trích thực thể - An Example of Entity Extraction

Chúng ta hãy xem xét một mẫu văn bản nhỏ từ một câu chuyện tin tức sau đây:

Cecilia Love, 52, a retired police investigator who lives in Massachusetts, said she paid around $370 a ticket with tax for nonstop United Airlines flights to Sacramento from Boston for her niece's high school graduation in June, 2020.

Chúng ta sẽ xem xét những thực thể named trong đoạn văn bản phía trên. Một thực thể named là bất cứ thứ gì có thể được tham chiều với một tên thích hợp: a person - một người, a location - một địa điểm, an organization - một tổ chức, … Việc xác định một thực thể được đặt tên thường được mở rộng để bao gồm những thứ không phải là thực thể, bao gồm ngày, giờ và các loại biểu thức khác liên quan đến thời gian và thậm chí cả biểu thức số học, ví dụ: giá

\[<sub>PER</sub>Cecilia Love\], 52, a retired police investigator who lives in \[<sub>LOC</sub>New Jersey\], said she paid around \[MONEY $370\] a ticket with tax for nonstop \[<sub>ORG</sub>United Airlines\] flight to \[<sub>LOC</sub>Sacramento\] from \[<sub>LOC</sub>Boston\] for her niece's high school graduation in \[<sub>TIME</sub> June, 2020\].

Đoạn văn bản chứa 7 thực thể được đặt tên, một trong số đó là một người - a person (được chỉ định bởi PER), ba trong số đó là địa điểm - location (được chỉ định bởi LOC), một trong số đó là tiền - money (được chỉ định bởi MONEY), một trong đó là tổ chức - organization (được chỉ định bởi ORG) và một trong đó là thời gian - time (được chỉ định bởi TIME). Phục thuộc vào phạm vi của ứng dụng, chúng ta có thể thêm nhiều hơn hoặc ít hơn những kiểu thuộc tính được đặt tên. Ví dụ, trong tác vụ định danh những thuật ngữ khoá trong một văn bản, chỉ có một loại thực thể biểu diễn một cụm từ khóa.

Tác vụ rút trích thực thể hữu ích trong nhiều ứng dụng. Ví dụ như, trong trả lời câu hỏi - question answering, nó có thể giúp lấy ra câu trả lời từ một đoạn văn bản được truy xuất. Trong một ứng dụng xử lý từ, nó có thể giúp trong liên kết một cách tự động những thực thể xuất hiện trong văn bản với những thông tin được thêm vào (như định nghĩa, dữ kiện, …) về những thực thể đó.

### 3.2 Những phương pháp tiếp cận cho rút trích thực thể - Approaches to Entity Extraction

Đầu tiên và quan trọng nhất, chúng ta có thể xem rút trích thực thể như một vấn đề gán nhãn. Chúng ta liên hệ một nhãn (label) với mỗi từ, và tác vụ này trở thành việc dự đoán nhãn. Chúng ta có thể thực hiện rút trích thực thể bằng ba phương pháp tiếp cận:

\- (1) Sequence labeling

\- (2) Deep Learning Models

\- (3) Rule-based Approaches

Chúng ta sẽ điểm qua từng phương pháp tiếp cận một

Để tạo điều kiện cho việc gán nhãn, chúng ta thêm vào một lược đồ gán nhãn được biết đến với tên là BIOES trong đó

\- B đại diện cho the beginning of an entity - Bắt đầu một thực thể

\- I đại diện cho the interior of an entity - Nội dung của một thực thể

\- O đại diện cho a word that is not part of an entity - Một từ không nằm trong một thực thể

\- E đại diện cho the end of an entity - Kết thúc một thực thể

\- S đại diện cho a single word entity - Một từ đơn mô tả thực thể

Lấy một ví dụ, những trong đoạn văn bản phía trên sẽ được gán nhãn như bảng được cho ở bên dưới

|         |   |          |   |               |   |              |   |            |   |
| ------- | - | -------- | - | ------------- | - | ------------ | - | ---------- | - |
| Cecilia | B | Love     | E | ,             | O | 52           | O | ,          | O |
| a       | O | retired  | O | police        | O | investigator | O | who        | O |
| lives   | O | in       | O | Massachusetts | S | ,            | O | said       | O |
| she     | O | paid     | O | around        | O | $370         | S | a          | O |
| ticket  | O | with     | O | tax           | O | for          | O | nonstop    | O |
| Untied  | B | Airlines | E | flights       | O | to           | O | Sacramento | S |
| from    | O | Boston   | S | for           | O | her          | O | niece’s    | O |
| high    | O | school   | O | graduation    | O | in           | O | June       | B |
| ,       | I | 2020     | E |               |   |              |   |            |   |

Với phương pháp tiếp cận Sequence Labeling - Chuỗi gán nhãn, chúng ta huấn luyện một thuật toán máy học (Machine Learning Algorithm), ví dụ như Conditional Random Fields - Trường điều kiện ngẫu nhiên), sử dụng những đặc trưng (features) như: part of speech - đoạn giọng nói, presence of the word in a list of standard words - hiện diện của một từ trong một danh sách từ chuẩn hoá, word embeddings, word base form, từ liệu có chứa một tiền tố (prefix) hay hậu tố (suffix), liệu từ có được in hoa toàn bộ, … Cần có sự nổ lực đáng để trong Feature Engineering - Kỹ thuật đặc trưng, bởi vì hiệu suất của việc lựa chọn những đặc trưng cụ thể và thuật toán máy học có thể thay đổi bởi phạm vi xem xét.

Với phương pháp tiếp cận Deep Learning - Học Sâu, ở đây không cần những kỹ thuật đặc trưng - feature engineering, và chúng ta đơn giản đưa word embeddings vào một mô hình ngôn ngữ (language model). Thay vì dự đoán xem từ kế tiếp là gì, mô hình ngôn ngữ bây giờ dự đoán một trong năm nhãn (tag) (B, I, O, E, S) cần cho việc nhận dạng thực thể (entity recognition). Để điều chính mô hình ngôn ngữ cho một tác vụ mới, đầu tiên chúng là huấn luyện trước nó sử dụng kho ngữ liệu cho miền đang xem xét, và sau đó huấn luyện nó cho tác vụ đang thực hiện. Trong những tác vụ xác định của mô hình ngôn ngữ, chúng ta cung cấp quá trình huấn luyện bằng cách thêm một token phân biệt (distinguished token) \[CLS\] mà đại diện cho điểm bắt đầu một thực thể (the beginning of an entity), và một token phân biệt thứ hai \[SEP\] đại diện cho điểm kết thúc một thực thể (the end of an entity). Quá trình huấn luyện cho phép mô hình dự đoán những nhãn phân biệt (distinguished tags) này để phản hồi một văn bản đầu vào. Những dự đoán như vậy là đủ cho chúng ta để tạo ra một trong năm nhãn cho mỗi từ.

Cuối cùng, với phương pháp tiếp cận Rule-Based - Dựa trên luật, một luật gán nhãn xác định (ne specifies labeling rules) trong một ngôn ngữ truy vấn hình thức (formal query language). Những luật này có thể bao gồm regular expression - biểu thức chính quy, references to dictionaries - tham chiếu tư điển, semantic constraints - ràng buộc ngữ nghĩa, và cũng có thể liên qua để bộ tự động rút trích và những cấu trúc bảng tham chiếu. Những luật này cũng có thể liên quan đến những module máy học cho những tác vụ cụ thể. Áp dụng luật có thể là một chuỗi trình tự theo cách mà đầu tiên chúng ta sử dụng những luật có precision cao (high precision rules), sau đó là tra cứu trong một danh sách tên chuẩn hoá, sau đó là dựa trên kinh nghiệm ngôn ngữ - language-based heuristics, và nếu sau tất cả đều thất bại, thì dùng để những kỹ thuật máy học xác suất (probabilistic machine learning techniques)

### 3.3 Những thách thức trong rút trích thực thể - Challenges in Entity Extraction

Mặc dù với những tác vụ xác định, các bộ rút trích thực thể (entity extractors) có thể cho thấy precision và recall trên 90% nhưng đạt được một hiệu suất tốt qua tất cả những miền (across all the domains) có thể là một thách thức. Trong phần này, chúng ta đề cập một thách thức mà chúng ta phải đối mặt trong quá trình rút trích thực thể .

Trong khi gán nhãn quan hệ với lớp của chúng, có rất nhiều trường hợp nhập nhằng (numerous cases of ambiguity). Ví dụ như, cho một thực thể Louis Vuitton, nó có thể tham chiếu đến một người - a person, hoặc một tổ chức - an organization, hoặc sản phẩm thương mai - am commercial product. Không thể giải quyết những vấn đề như sự nhập nhằng nếu như không tính đến ngữ cảnh một cách đáng kể.

Với cách sử dụng một mô hình học máy (machine learning model), chúng ta lượng dữ liệu cực kỳ to lớn. Trong thực tế, dữ liệu thường không có sẵn hoặc phần lớn chúng chưa hoàn thiện. Khi chúng ta huấn luyện mô hình sử dụng dữ liệu không hoàn thiện, nó sẽ ảnh hưởng nghiêm trọng đến hiệu suất.

Một trong những biến thể của rút trích thực thể là định danh những cụm từ khoá trong văn bản. Vì những cụm từ khoá là không giới hạn ở một số lớp, tác vụ định danh những lớp xác định tương ứng với một cụm từ khoá có thể trở nên thách thức hơn. Thỉnh thoảng, những cụm từ khoá quá phức tạp (overly complex) (ví dụ: duplication of a cell by fission), và đôi khi quá chung chung (too general) (ví dụ như: Attach) làm cho tác vụ này quá khó để mà áp dụng một kỹ thuật thống nhất trên diện rộng.

Những thực thể có thể xuất hiện ở nhiều hình dạng khác nhau (different surface forms), ví dụ như: synonyms - từ đồng nghĩa, acronyms - từ viết tắt, plurals - dạng số nhiều và morphological variations - các biến thể hình thái :)))))))))????. Nói chung, rút trích thực thể cần chú trọng về tri thức từ vựng (lexical knowledge) mà thường không tồn tại khi vào một lĩnh vực/ miền mới. Do đó, việc cải thiện hiệu năng của rút trích thực thể, rút trích từ vựng (lexicon extraction) trở thành một tác vụ liên quan thiết yếu.

## 4\. Rút trích quan hệ - Relation Extraction

Chúng ta sẽ bắt đầu bằng cách đề cặp một vài ví dụ cụ thể về rút trích quan hệ, sau đó tìm hiểu một cách tổng quan về những phương pháp tiếp cận khác nhau cho rút trích quan hệ, và kết lại phần này bằng cách thảo thuận một số thách thức làm sao đạt hiệu suất tốt với tác vụ này.

### 4.1 Ví dụ về rút trích quan hệ - Examples of Relation Extraction

Xem xét đoạn văn bản từ phần trước, chúng ta có thể rút trích những quan hệ như Cecilia Love *lives* in Massachusetts, United Airlines *flies* from Boston và United Airlines *flies* to Sacramento, … Trong một tác vụ rút trích quan hệ thông thường, những thực thể đã được định danh trước đó, và trong trường hợp này, nó mở rộng tác vụ rút trích thực thể. Những quan hệ sẽ được rút trích cũng được xác định trước đó.

Một thể hiện thể phổ biến của tác vụ rút trích quan hệ là rút trích những thông tin từ Wikipedia Infoboxes. Ứng dụng rõ ràng của tác vụ này là cải thiện kết quả tìm kiếm trên Internet. Wikipedia infoboxes định nghĩa những mối quan hệ như preceded by, succeeded by, children, spouse, … Đạt được một độ chính xác cao (a high accuracy) đối với tác vụ này có thể là một thách thức bởi một lượng lớn những trường khó (corner cases). Ví dụ, Larry King đã kết hôn nhiều lần, do đó bộ rút trích phải có khả năng lấy ra những thông tin khoảng thời gian mà cuộc hôn nhân tồn tại.

Ở đây cũng tồn tại những miền xác định những mối quan hệ. Ví dụ, Unified Medical Language Systems hỗ trợ những mối quan hệ như causes, treats, disrupts, … Ngoại trừ những quan hệ chuẩn hoá như subclass-of, has\_part, những mối quan hệ sẽ được rút trích là những miền xác định và thường yêu cầu một số thiết kế từ trước. Có một số phương pháp tiếp cận để rút trích quan hệ mà không yêu cầu lựa chọn những quan hệ từ trước, nhưng tính hữu ích của những phương pháp như vậy trong thực tế được phát hiện là bị giới hạn.

### 4.2 Những phương pháp tiếp cận cho rút trích quan hệ - Approaches to Relation Extraction

Có ba phương pháp diện rộng để rút trích quan hệ:

\- (1) syntactic patterns

\- (2) various forms of supervised machine learning

\- (3) unsupervised machine learning

Như được đề cập từ phần trước, unsupervised machine learning bị giới hạn sử dụng trong thực tế. Do đó chúng ta sẽ xem xét chủ yếu việc sử dụng syntactic patterns và supervised machine learning cho việc rút trích quan hệ.

Một phương pháp tiếp cận kinh điển cho rút trích quan hệ dựa trên syntactic patterns được biết đến như Hearst Patterns. Ví dụ, xem xét câu dưới đây:

The bow lute, such as the Bambara ndang, is plucked and has an individual curved neck for each string.

Cho dù chúng ta chưa từng được nghe đến Bambara ndang, chúng ta vẫn có thể suy luận nó là một loại đàn nguyệt hình cung (a kind of bow lute, lute là một danh từ có nghĩa là đàn nguyệt, đờn tỳ bà, bow: cây cung). Tổng quát hơn, chúng ta có thể định danh syntactic patterns - mẫu cú pháp mà có những chỉ số cao về subclass của mối quan hệ. Năm mẫu cú pháp sau đây đã xuất hiện khá lâu và cực kỳ hiệu quan trong thực tế.

|              |                                                                    |
| ------------ | ------------------------------------------------------------------ |
| Pattern Name | Example                                                            |
| such as      | ... works by authors such as Herric, Goldsmith, and Shakespear ... |
| or other     | Bruises, wounds, broken bones, or other injuries ...               |
| and other    | .. temples, treasuries, and other Civic Buildings, ...             |
| including    | All common law countries including Canada and England ...          |
| especially   | Most European countries especially France, England, and Spain, ... |

Chúng ta có thể khám pháp những mẫu cú pháp mới cho bất kỳ mối quan hệ nào như sau. Đầu tiên, chúng thu gom những mẫu cho mối quan hệ được cho là đúng. Sau đó, chúng ta tìm những câu mà mối quan hệ là đúng. Bằng cách xác định những điểm chung thông qua những câu đó, chúng ta có thể định nghĩa ra được một mẫu mới. Chúng ta có thể kiểm tra những mẫu (patterns) dựa trên kho ngữ liệu. Một thuật toán như thế được gọi là Dual Iterative Pattern Relation Expansion (DIPRE).

Chúng ta cụ thể hoá nguyên lý hoạt động của nó bằng một vấn đề của việc rút trích cặp (author, title) từ một kho ngữ liệu. Chúng ta bắt đầu với một tập các cặp (author, title) đã được biết, và chúng ta tìm tất cả số lần xuất hiện của chúng trong bộ ngữ liệu, và từ những thứ đó chúng ta tạo ra nhiều mẫu hơn. Thuật toán tiếp tục một cách đệ quy bằng cách sử dụng những mẫu mới để khám phá nhiều sách hơn, và từ việc khám phá những mẫu mới của chúng. Một ví dụ cụ thể, cho một cặp (William Shakespear, The Comedy of Errors), và những câu sau:

\- The Comedy of Errors, by William Shakespeare, was …

\- The Comedy of Errors, by William Shakespeare, is …

\- The Comedy of Errors, one of William Shakespeare's earliest attempts …

\- The Comedy of Errors, one of William Shakespeare's most …

Chúng ta có thể thu được những mẫu (patterns) sau:

\- $?x , by ?y$

\- $?x , \\text{one of } ?y’s$

Bằng cách sử dụng những mẫu mới thu được, quá trình rút trích tiếp tục một cách đệ quy.

Phương pháp tiếp cận supervised - có giám sát cho rút trích quan hệ cần dữ liệu huấn luyện phong phú. Bất cứ khi nào dữ liệu huấn luyện là sẵn có, nhiều thuật toán học có sẵn (the off-tbe-shelf) có thể được huấn luyện. Nhưng, trong trường hợp không đủ dữ liệu, tiếp cận giám sát yếu (weak supervision approaches) trở nên phổ biến để giải quyết yêu cầu về dữ liệu. Ý tưởng cơ bản trong weak supervision là sử dụng nhiều hàm gán nhãn gần đúng (several approximate labeling functions) mà có thể tạo ra dữ liệu huấn luyện một cách tự động. Những nhãn yếu (weak labels) này có thể được kết hợp bằng cách sử dụng một hàm xác suất (probabilistic function)

Một ví dụ về một hàm gán nhãn yếu (a weak labeling function), xem xét quan hệ has\_part. Với quan hệ này, nó không có khả năng để phát triển những mẫu cú pháp (syntactic patterns) của loại được đề xuất như trên. Một hàm gán nhãn yếu (weak labeling function) có thể có cho mối quan hệ này là đầu tiên tạo ra một phân tích cú pháp phụ thuộc cho câu, và sau đó tìm kiếm hai node trong phân tích mà có một đường đi chiều dài một chứa động từ has hoặc have. Với mối quan hệ taxonomic (mối quan hệ phân loại), một hàm gán nhãn yếu (weak labeling function) bổ sung nếu hai thực thể kết thúc với cùng một từ cơ sở nhưng một trong chúng có một cụm bổ nghĩa ( additional modifier) đứng trước nó, điều này gợi ý một taxonomic relation (ví dụ như: eukaryotic cell SUBCLASS cell).

Để điều chỉnh một mô hình ngôn ngữ cho tác vụ rút trích quan hệ, chúng ta thay đổi biểu diễn đầu vào của một câu để mà mỗi một thuật ngữ cá thể được đánh dấu một cách rõ ràng. Ví dụ: chúng ta đưa vào một câu như \["All", "\[TERM1-START\]", "cells", "\[TERM1-END\]", "have", "a", "\[TERM2-START\]", "cell" "membrane", "\[TERM2-END\]", "."\], và kỳ vọng mô hình cho ra phân phố xác suất trên những mối quan hệ khác nhau, điều này có thể tồn tại hai thuật ngữ. Mối quan hệ dự đoán được phụ thuộc vào dữ liệu huấn luyện đầu vào.

### 4.3 Những thách thức trong rút trích quan hệ

Thách thức chính trong rút trích quan hệ là có được lượng dữ liệu huấn luyện cần thiết. Phương pháp tiếp cận giám sát yếu (weak supervision approach) khá là hứa hẹn bởi dữ liệu huấn luyện không cần phải hoàn thiện. Chúng ta có thể dùng đến những nguồn như Wikidata và Wordnet như một nguồn dữ liệu cho việc định nghĩa những hàm gán nhãn yếu (weak labeling functions). Phát triển một phương pháp tiếp cận mới cho weak labeling functions là một chủ đề đã và đang tiến hành nghiên cứu.

Chúng ta cũng cần có một quy trình làm việc (workflow) tốt để mà xác nhận những kết quả từ các bộ rút trích. Những bộ rút trích thường xuyên được tạo ra bởi cộng đồng (crowdsourcing). Chúng ta cũng có thể ưu tiên xác nhận những quan hệ rút trích được mà có độ tin cậy thấp. Phát triển các vòng lặp active learning là một thách thức khác hiện đang được nghiên cứu.

## 5\. Tổng kết

Với chương này, chúng ta đề cập đến vấn đề khởi tạo một đồ thị tri thức bằng cách xử lý văn bản. Chúng ta điểm qua hai vấn đề cơ bản là rút trích thực thể (entity extraction) và (relation extracion). Với cả hai tác vụ này, những công trình trước đây tập trung vào xác định những quy tác thủ công và cú pháp cho việc rút trích. Những phương pháp tiếp cận gần đây dựa trên điều đỉnh mô hình ngôn ngữ được huấn luyện sẵn (pre-trained language models) và tinh chỉnh chúng cho những bộ ngữ liệu cụ thể ở công việc đang xử lý.

Với cả rút trích thực thể và rút trích quan hệ, cách tiếp cận phổ biến nhất hiện nay là điều chỉnh một mô hình ngôn ngữ được tạo ra trước bằng cách sử dụng Học Sâu (Deep Learning). Cũng có những phương pháp tiếp cận, dựa trên cú pháp (syntactic) hay dựa trên luật (rule-based) cũng đóng vai trò quan trong trong boostrapping dữ liệu huấn luyện cần cho mô hình Học Sâu (Deep Learning). Việc xác nhận đầu ra của rút trích tiếp tục là một thách thức.

Vấn đề liên kết thực thể (entity linking) hay phân giải thực thể (entity resolution) là một vấn đề quan trong không kém trong việc khởi tạo đồ thị tri thức, nhưng chúng ta không đề cập đến nó trong phần thảo luận này bởi hai lý do:

\- Lý do thứ nhất, chúng ta tin rằng thách thức cho việc có được hiệu năng tốt là nằm ở rút trích thực thể (entity extraction) và rút trích quan hệ (relation extraction), chính nó là một rào cản đáng kể

\- Lý do thứ hai, một điều kiện tiên quyết để có một hiệu suất tốt trên liên kết thực thể (entity linking) là có sẵn một vốn từ vựng tốt

Với những lý do này, phân giải thực thể (entity resolution) là một kỹ thuật nâng cao (an advanced technique) và nó có thể hoặc không là nút thắc trong giải quyết vấn đề khởi tạo đồ thị.

**Bài tập:**

...Sẽ cập nhật sau…

Bài giảng gốc: https://web.stanford.edu/class/cs520/2020/notes/How\_To\_Create\_A\_Knowledge\_Graph\_From\_Text.html
 thêm vào. Nhưng với sự giúp đỡ của việc định nghĩa nó bằng cách dùng một luật, một rule engine có thể tính toán xung đột của quan hệ quan tâm đến coi. Trong một vài trường hợp, chúng ta có thể quan đến việc thêm vào những giá trị đã được tính toán của quan hệ coi vào đồ thị tri thức của chúng ta. Vì coi là quan hệ ba ngôi, chúng ta sẽ cần phải tái tổ chức nó. Vì tái tổ chức yêu cầu thêm vào những đối tượng mới trong đồ thị, chúng ta có thể xác định chúng bằng cách sử dụng một quy luật tồn tại được cho bên dưới:

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
