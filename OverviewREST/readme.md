**API (Application Programming Interface)** là một tập các quy tắc và cơ chế mà theo đó, một ứng dụng hay một thành phần sẽ tương tác với một ứng dụng hay thành phần khác. API có thể trả về dữ liệu mà bạn cần cho ứng dụng của mình ở những kiểu dữ liệu phổ biến như JSON hay XML.

**REST (REpresentational State Transfer)** là một dạng chuyển đổi cấu trúc dữ liệu, một kiểu kiến trúc để viết API. Nó sử dụng phương thức HTTP đơn giản để tạo cho giao tiếp giữa các máy. Vì vậy, thay vì sử dụng một URL cho việc xử lý một số thông tin người dùng, REST gửi một yêu cầu HTTP như GET, POST, DELETE, vv đến một URL để xử lý dữ liệu.

**RESTful API** là một tiêu chuẩn dùng trong việc thiết kế các API cho các ứng dụng web để quản lý các resource. RESTful là một trong những kiểu thiết kế API được sử dụng phổ biến ngày nay để cho các ứng dụng (web, mobile…) khác nhau giao tiếp với nhau.

### Tổng quan những gì chúng ta sẽ tìm hiểu

![enter image description here](https://miro.medium.com/max/630/1*lFGlOSW19H184tUt9DhvUg@2x.png)

## 1. Nguyên tắc của REST

Sáu nguyên tắc hoặc rằng buộc của kiến trúc `RESTful` là :

### 1.1 Uniform Interface ( Giao diện thống nhất )

Bằng cách áp dụng nguyên tắc tổng quát (Một nhóm quy tắc chung của kỹ thuật phần mềm : chi tiết có thể đọc tại [đây](https://www.d.umn.edu/~gshute/softeng/principles.html) ) cho các thành phần, chúng ta có thể đơn giản hóa kiến ​​trúc hệ thống tổng thể và cải thiện khả năng hiển thị của các tương tác.

Bốn rằng buộc sau đây có thể đặt được để thống nhất REST Interface :

![](../images//Screenshot%20from%202022-09-19%2000-50-13.png)

- **Identification of resources** : Interface sẽ phải định danh các tài nguyên tương tác giữa client và server ( lưu ý các tài nguyên này sẽ phải là duy nhất )
- **Manipulation of resources through representations** : Các tài nguyên phải có các đại diện thống nhất trong Respon của máy chủ. Client sẽ sử dụng chuẩn này để giao tiếp với máy chủ
- **Self-descriptive messages** : Mỗi biểu diễn tài nguyên phải mang đủ thông tin để mô tả cách xử lý thông báo. Nó cũng phải cung cấp thông tin về các hành động bổ sung mà khách hàng có thể thực hiện trên tài nguyên.
- **Hypermedia as the engine of application state - HATEOAS** : Client chỉ nên có URI ban đầu của ứng dụng. Ứng dụng khách sẽ tự động điều khiển tất cả các tài nguyên và tương tác khác với việc sử dụng hyperlinks.

### 1.2 Client-Server

Mẫu thiết kế máy khách-máy chủ thực thi sự tách biệt các mối quan tâm, giúp máy khách và các thành phần máy chủ phát triển độc lập.

Bằng cách tách mối quan tâm về giao diện người dùng (máy khách) khỏi mối quan tâm về lưu trữ dữ liệu (máy chủ), chúng tôi cải thiện tính di động của giao diện người dùng trên nhiều nền tảng và cải thiện khả năng mở rộng bằng cách đơn giản hóa các thành phần máy chủ.

Trong khi máy khách và máy chủ phát triển, chúng tôi phải đảm bảo rằng giao diện / hợp đồng giữa máy khách và máy chủ không bị phá vỡ.

### 1.3 Stateless

`Stateless` : yêu cầu mỗi request từ client đến server phải chứa tất cả các thông tin cần thiết để hiểu và hoàn thành request.

server không thể tận dụng thông tin ngữ cảnh từ request trước đó

với lý do này thì client phải dữ được session state

### 1.4 Cacheable

Rằng buộc yêu cầu phải dán nhãn rõ ràng Respon phải dán nhẵn rõ ràng có thể lưu vào bộ nhớ cache hay không

Trong trường hợp cache respon , client có quyền sử dụng lại dữ liệu phản hồi sau đó cho các yêu cầu tương đương và trong một khoảng thời gian cụ thể.

### 1.5. Layered System

Kiểu hệ thống phân lớp cho phép một kiến ​​trúc bao gồm các lớp phân cấp bằng cách hạn chế hành vi của thành phần.
Ví dụ, trong một hệ thống phân lớp, mỗi thành phần không thể nhìn thấy ngoài lớp ngay lập tức mà chúng đang tương tác.

### 1.6. Code on Demand (_Optional_)

REST cũng cho phép mở rộng chức năng máy khách bằng cách tải xuống và thực thi mã dưới dạng các applet hoặc script.
Mã đã tải xuống sẽ đơn giản hóa ứng dụng bằng cách giảm số lượng các tính năng bắt buộc phải triển khai trước.Server có thể cung cấp một phần các tính năng được giao cho client dưới dạng mã và máy khách chỉ cần thực thi mã.

## Các yêu cầu chính cho API
Nhiều ý kiến trong việc thiết kế API được tìm thấy trên mạng hầu hết là các cuộc thảo luận học thuật xoay quanh việc diễn giải các tiêu chuẩn mơ hồ và trái ngược lại với những gì có ý nghĩa trong thực tiễn. Mục tiêu của tôi trong bài viết này là mô tả một best practices cho một pragmatic API được thiết kế cho các ứng dụng web tại thời điểm hiện tại. Tôi sẽ ko cố gắng để thoả mãn một tiêu chiểu nào đó nếu cảm giác rằng nó ko đúng. Để theo sát quá trinh đưa ra quyết đinh, tôi đã viết ra một số yêu cầu mà API phải có :

Nên sử dụng các tiêu chuẩn web khi cần thiêt
Nên thân thiệt với developer và có thể sử dụng được thông qua thanh nhập địa chỉ của browser
Nên đơn giản. trực quan và nhất quán để làm cho việc áp dụng vừa đơn giản vừa dễ dàng
Nên flexible để có thể đáp ứng các yêu cầu về UI
Nên hiệu quả, trong khi duy trì sự cần bằng với các yêu cầu khác
Một API chính là một UI của developer - cũng giống như bất kì UI nào, điều quan trọng là phải cân nhắc đầy đủ về trải nghiệm của người dùng.

Sử dụng RESTful URLs và các actions
RESTful là 1 chuẩn đã được áp dụng cực kì rộng rãi. Chuẩn này lần đầu tiên được ứng dụng bởi Roy Fielding trong chường 5 của luạn án về kiến trức phần mềm dựa trên network của ông.

Các nguyên tắc chính của REST liên quan đến việc tách API của bạn thành các tài nguyên hợp lý. Các tài nguyên này được quản lý và vận hành/thao tác bằng cách sử dụng các request HTTP, trong đó các method (GET, POST, PUT, PATCH, DELETE) có một ý nghĩa cụ thể.

Nhưng tôi có thể tạo ra tài nguyên nào? Vâng, đây là những danh từ (chứ không phải động từ) có ý nghĩa từ quan điểm của người sử dụng API. Mặc dù các mô hình nội bộ của bạn có thể được sắp xếp gọn gàng với các tài nguyên, nhưng nó không nhất thiết phải được mapping one-to-one. Chìa khóa ở đây là không rò rỉ các chi tiết implementation không liên quan đến API của bạn! Một số danh từ của ứng dụng Enchant có thể là ticket, user và group.

Khi bạn đã xác định được các tài nguyên của mình, bạn cần phải xác định những hành động nào áp dụng cho chúng và cách các tài nguyên đó map vào API của bạn. Các nguyên tắc RESTful cung cấp các chiến lược để xử lý CRUD bằng cách sử dụng HTTP method được map như sau :
```js
GET /tickets - Nhận một list các tickets
GET /tickets/12 - Nhận một ticket cụ thể
POST /tickets - Tạo một ticket mới
PUT /tickets/12 - Update ticket #12
PATCH /tickets/12 - Update 1 phần ticket #12
DELETE /tickets/12 - Xoá ticket #12
Điều tuyệt vời ở REST là bạn đang tận dụng các phương thức HTTP hiện có để thực hiện các chức năng quan trọng trên chỉ trên một endpoint /tickets. Không có quy ước naming convention để làm theo và cấu trúc URL là rất tường minh và rõ ràng.
```
Tên của endpont có phải là số ít hoặc số nhiều không? Nguyên tắc keep-it-simple được áp dụng ở đây. Mặc dù các nhà ngôn ngữ học về ngữ pháp của bạn sẽ cho bạn biết rằng đó là sai khi mô tả một tài nguyên bằng cách sử dụng số nhiều, nhưng câu trả lời là hãy giữ định dạng URL nhất quán và luôn sử dụng số nhiều. Không phải đối phó với các trường hợp số nhiều đặc biệt cuả tiếng Anh ( person/people, goose/geese) làm cho người áp dụng API thoải mái hơn và dễ dàng hơn cho nhà cung cấp API để thực hiện (/tickets và /tickets/12 được xử lý cùng 1 controller).

Làm thế nào để bạn đối phó với các quan hệ? Nếu các quan hệ chỉ có thể tồn tại trong một tài nguyên khác, các nguyên tắc RESTful cung cấp các chuẩn rất tiên lợi. Hãy xem xét điều này bằng một ví dụ. Một ticket trong Enchant bao gồm một số messages. Các messages có thể được map tới endpoint /tickets như sau :
```js
GET /tickets/12/messages - Lấy danh sách messages cho ticket # 12
GET /tickets/12/messages/5 - Lấy message số 5 cho ticket 12
POST /tickets/12/messages - Tạo một message mới trong ticket #12
PUT /tickets/12/messages/5 - Update một message số #5 trong ticket #12
PATCH /tickets/12/messages/5 - Update một phần message #5 trong ticket #12
DELETE /tickets/12/messages/5 - Delete message #5 trong ticket 
```

Ngoài ra, nếu quan hệ có thể tồn tại độc lập với tài nguyên, bạn nên inclue identifier của nó trong output của tài nguyên. Người sử dụng API sau đó sẽ xử lý đến endpoint của quan hệ. Tuy nhiên, nếu quan hệ thường được yêu cầu cùng với tài nguyên, API nên cung cấp các chức năng để tự động nhúng bản thể của quan hệ và tránh lần truy cập thứ hai vào API.

Làm sao nếu actions không khớp với CRUD ?

Có một số cách tiếp cận:

Cơ cấu lại các actions để thao tác với các field của nguồn tài nguyên. Nếu action ko yêu cầu parameter thì việc này sẽ có tác dụng. Ví dụ, một action kích hoạt có thể được map tới một trường có type là boolean và được cập nhật thông qua PATCH tới tài nguyên.

Xử lý nó như một nguồn tài nguyên phụ với các nguyên tắc RESTful. Ví dụ: API của GitHub cho phép bạn gắn dấu sao với PUT /gists/:id/star và bỏ dấu sao bằng DELETE /gists/:id/star.

Đôi khi bạn thực sự không có cách nào để map action đến một cấu trúc RESTful hợp lý. Ví dụ, một action tìm kiếm nhiều tài nguyên không thực sự có ý nghĩa để được áp dụng endpoint tới một tài nguyên cụ thể. Trong trường hợp này, /search sẽ có ý nghĩa nhất mặc dù nó không phải là tài nguyên. Điều này là OK - chỉ cần làm những gì bạn cảm thấy đúng từ quan điểm của sử dụng API và đảm bảo rằng nó được giải thích - làm tài liệu rõ ràng để tránh nhầm lẫn.

SSL ở mọi nơi - mọi lúc
Luôn luôn sử dụng SSL. Không có ngoại lệ. Ngày nay, các API web của bạn có thể được truy cập từ mọi nơi có internet (như thư viện, quán cà phê, sân bay). Không phải tất cả những điều này đều an toàn. Và có rất nhiều nơi không mã hóa thông tin liên lạc, khiến cho việc dễ dàng nghe trộm hoặc giả mạo nếu thông tin xác thực bị tấn công.

Một ưu điểm khác của việc sử dụng SSL là một communication được mã hóa sẽ khiến việc xác thực trở nên đơn giản hơn rất nhiều - bạn có thể authen bằng các access token thay vì việc phải ký vào từng API request.

Một điều cần lưu ý là hãy warning các access sủ dụng non-SSL tới các URL API. Không chuyển hướng chúng đến các đối tác SSL. Hãy trả về lỗi nếu có thể ! Điều cuối cùng bạn cần làm cho các máy client được cấu hình kém là redirect các yêu cầu không được mã hóa tới endpoint được mã hoá thực sự.

Tài liệu
Một API cần phải chuẩn cũng như các tài liệu giải thích về nó. Các tài liệu nên dễ tìm kiếm và truy cập được. Hầu hết các nhà phát triển sẽ kiểm tra các tài liệu trước khi thử tích hợp. Khi tài liệu ẩn bên trong tệp PDF hoặc yêu cầu đăng nhập, chúng không chỉ khó tìm mà còn không dễ tìm kiếm.

Các tài liệu nên bao gồm cả ví dụ về một request/response hoàn chỉnh sẽ trông như thế nào. Một cách hoàn hảo, request nên có các ví dụ các thể copy - paste được ( url vào browser hoặc curl vào terminal). Github và Stripe thực sự đã làm việc này rất tốt.

Khi bạn phát hành một API public, bạn đã cam kết không thay đổi điều gì mà không thông báo. Tài liệu phải bao gồm bất kỳ lịch thay đổi / loại bỏ nào và chi tiết xung quanh các bản cập nhật API. Thông tin cập nhật phải được gửi qua blog (ví dụ như changelog) hoặc danh sách thư (tốt nhất cả hai!).

Versioning
Luôn luôn đánh phiên bản API của bạn. Phiên bản giúp bạn iterate nhanh hơn và ngăn các yêu cầu không hợp lệ khi truy cập vào các endpoint đã được update. Nó cũng giúp làm nuột quá trính thay đổi phiên bản API chính nào trong khi bạn có thể tiếp tục cung cấp các phiên bản API cũ trong một khoảng thời gian.

Có nhiều ý kiến trái chiều khác nhau về việc có nên include phiên bản API trong URL hoặc trong header. Về mặt học thuật, thì nên là header. Tuy nhiên, phiên bản nên được có trong URL để đảm bảo khả năng khám phá của trình duyệt đối với tài nguyên qua các phiên bản

Tôi là một fan hâm mộ lớn của cách tiếp cận mà Stripe đã thực hiện để versioning APIs. Các URL của họ có số phiên bản chính (v1), nhưng API có các phiên bản phụ dựa trên ngày có thể được chọn bằng cách custom HTTP request header. Trong trường hợp này, phiên bản chính cung cấp sự ổn định về cấu trúc của API như một toàn bộ trong khi các phiên bản phụ cho thấy thay đổi nhỏ hơn (bỏ trường, thay đổi endpoint, vv).

Một API sẽ không bao giờ được hoàn toàn ổn định. Thay đổi là không thể tránh khỏi. Điều quan trọng là làm thế nào thay đổi này được quản lý một cách cẩn thận. Các tài liệu cuẩn và các thông báo deprecation được lên lịch trước nhiều tháng sẽ là các practice được chấp nhận đối với nhiều APIs.

Filtering, sorting & searching kết quả
Tốt nhất nên giữ cho các URL của các tài nguyên cơ bản càng gọn gàng càng tốt. Một bộ lọc, yêu cầu sort, search nâng cao quá phức tạp có thể được implement dễ dàng dưới dạng các parameter query trong base URL. Hãy nhìn vào chi tiết hơn việc này :

Filtering : Sử dụng một param unique cho mỗi mỗi trường cần implement filteing. Ví dụ, khi một request list các tickets từ endpoint /tickets , bạn sẽ uốn giới hạn số lượng tickets được trả về là phải ở trang thái open. Nó có thể được thực hiện với một request GET như sau GET /tickets?state=open. Ở đây state chính là param thực hiện việc filter.

Sorting Tương tự với filtering, một param chung sort có thể được sử dụng để mô tả rule sort. Đảm bảo các yêu cầu sort phức tạp bằng cách cho phép các param sort nằm trong danh sách cách nhau bởi dấu phẩy, mỗi ô có thể là một số ấm để thể hiện thứ tự giảm dần. Hãy xem các ví dụ dưới đây :

GET /tickets?sort=-priority- Lấy list các tickets theo thứ tự giảm dần
GET /tickets?sort=-priority,created_at - Lấy list các tickets theo thứ tự giảm dần theo created_at
Searching Thỉnh thoảng, các filter cơ bản sẽ là ko đủ, bạn cần search text. Có thể bạn đã sử dụng ElasticSearch hoặc các công nghệ tìm kiếm dưạ trên Lucene khác. Khi một full text search được sử dụng như một cơ chế để lấy dữ liệu tài nguyên đối với loại tài nguyên cụ thể, thì nó có thể được hiển thị trên API như là một param query trên endpoint của tài nguyên. Hãy truyền vào param q. Search query sẽ được truyền thẳng tới search engine và API output sẽ có cùng format với list kết quả thông thường.

Kết hợp lại, ta có thể có các query như thế này :

GET /tickets?sort=-updated_at - Lấy list các tickets được update gần đây
GET /tickets?state=closed&sort=-updated_at - Lấy list các ticket được update close gần đây
GET /tickets?q=return&state=open&sort=-priority,created_at - Lấy các open tickets với ưu tiên ngày created_at và có chữ cái 'return'
**Aliases cho các query phổ biến **

Để làm cho trải nghiệm API trở nên dễ chịu hơn cho người sử dụng, hãy cân nhắc việc đóng gói các điều kiện vào các đường dẫn RESTful dễ tiếp cận. Ví dụ: truy vấn các tickets gần đây đã đóng gần đây có thể được đóng gói thành GET /tickets/recently_closed

Giới hạng các trường được return từ APIs
Người sư dụng API không phải lúc nào cũng cần đầy đủ tài nguyên. Khả năng lựa chọn và chọn các trường trong respnse lại là một cách lâu dài để cho phép người tiêu dùng API giảm thiểu lưu lượng mạng và đẩy nhanh việc tích hợp API của họ.

Sử dụng một param truy vấn trường để lấy danh sách các trường được phân cách bằng dấu phẩy để đưa vào. Ví dụ: yêu cầu sau đây sẽ lấy đủ thông tin để hiển thị danh sách được sắp xếp của các ticket open :

GET /tickets?fields=id,subject,customer_name,updated_at&state=open&sort=-updated_at

Updates & Tạo mới nên return một thực thể tài nguyên
Một request PUT, POST hoặc PATCH có thể thực hiện sửa đổi các trường của tài nguyên ngầm mà không phải là một phần của các tham số được cung cấp (ví dụ: created_at hoặc updated_at). Để ngăn không cho người sử dụng API phải gọi lại API một lần nữa cho một thực thể được cập nhật, hãy trả lại trong resqonse API giá trị của tài nguyên đã được cập nhật (hoặc được tạo).

Trong trường hợp POST tạo kết quả, hãy sử dụng mã trạng thái HTTP 201 và include header Location chỉ định URL của tài nguyên mới.

Có nên HATEOAS ?
Có rất nhiều ý kiến trái chiều khác nhau về việc liệu người sử dụng API nên tạo liên kết hay liệu liên kết nên được cung cấp cho API hay không. Nguyên tắc thiết kế RESTful đã chỉ định HATEOAS .

Mặc dù web thường hoạt động theo nguyên tắc loại HATEOAS (chúng ta truy cập đến trang chủ của trang web và theo các liên kết dựa trên những gì chúng ta thấy trên trang), tôi không nghĩ chúng ta đã làm chuẩn các yêu cầu HATEOAS trên APIs chưa. Có một ví dụ kiểu tương tự mà bạn có thể sẽ hình dung đến khi tìm hiểu những khái niệm này. Khi bạn vào một tờ báo, bạn sẽ thấy một danh sách tóm tắt các bài mới. Bạn đọc bài viết đầy đủ bằng cách bấm vào liên kết. Bạn không cần quan tâm ID của bài báo là gì, hay URI pattern của trang web là như thế nào. Bạn chỉ cần biết một điểm cuối duy nhất là URL của bài báo, từ đó bạn có thể đi khắp nơi. Tuy nhiên, với API, các quyết định về yêu cầu sẽ được gửi đi khi code chạy gọi API , chứ không phải tại thời gian chạy. Liệu các yêu cầu gọi API có thể bị trì hoãn trước thời gian chạy ko? Nói chung thì việc áp dụng nguyên tắc HATEOAS vào là vẫn là khá khó và tốn rất nhiều effort.

Tại thời điểm hiện tại, tốt nhất bạn nên cho rằng người sử dụng có thể quyền truy cập vào tài liệu API cũng như các identifier của các tài nguyên sẽ sử dụng khi tạo các liên kết. Có một vài lợi thế khi stick với identifier - dữ liệu trao đổi được giảm thiểu và dữ liệu được lưu trữ bởi người sử dụng API cũng được giảm thiểu (vì chúng đang lưu trữ các identifier nhỏ hơn rất nhiều so với các URL có chứa identifier).

Ngoài ra, với việc khuyến khích versioning trong URL, sẽ có ý nghĩa hơn về lâu dài đối với người sử dụng API để lưu trữ mã identifier của tài nguyên thay vì URL. Xét cho cùng, identifier là ổn định trên các phiên bản nhưng URL đại diện cho nó thì không.

Chỉ trả về JSON
Đã đến lúc phải từ bỏ XML. Khó để parse, khó read, data model không phù hợp với hầu hết các ngôn ngữ lập trình và khả năng mở rộng là ko thích hợp khi bạn cần serialization.

Tôi sẽ ko cố gắng giải thích nhiều về như vấn đề trên. Thực tế thì Youtube, Twitter, Box đã bắt đầu từ bỏ XML. Hãy xem biểu đồ Google Trends về XML API và JSON API :

alt

Tuy nhiên, nếu KH của bạn bao gồm một số lượng lớn các khách hàng doanh nghiệp, có thể bạn sẽ phải support XML. Nếu phải phải làm việc này, hãy thử trả lời câu hỏi sau : "Liệu type của một media thay đổi dựa trên Accept header hay là URL ?" . Nó sẽ là URL. Lựa chọn hợp lý ở đây sẽ là thêm vào sau URL extension .json hoặc .xml.

snake_case hay camelCase cho tên trường
Nếu bạn dùng JSON, điều bạn phải làm là follow naming conventions của JavaScript. Có nghĩa là camelCase cho tên trường. Hoặc bạn nên sử dụng các quy ước đặt tên theo ngôn ngữ mà bạn build các route - camelCase cho C# và Java, snake_case cho python và ruby.

Ý kiến cá nhân thì tôi luôn cảm thấy snake_case dễ đọc hơn camelCasse. Dựa vào một số nghiên cứu theo dõi mắt về camelCase và snake_case từ năm 2010, snake_case dễ đọc hơn 20% so với camelCase. Khả năng dễ đọc này sẽ tác động đến việc người sử dụng API đọc tài liệu APIs. HIện nay, rất nhiều APIs JSON nổi tiếng sử dụng snake_case.

Print by default & sử dụng GZIP
Một API trả dữ liệu trắng tinh nén trên browser thì hoàn toàn ko thú vị chút nào. Mặc dù có một vài param như (pretty=true) có thể được sử dụng để enable việc trả dữ liệu, nên setting nó thành default để dễ tiếp cận hơn. Cost của việc truyền thêm dữ liệu là không đáng kể đặc biệt khi bạn so sanh với cost của việc không tích hợp gzip.

Hãy xem xét một trường hợp cụ thể : Điều gì sẽ xảy ra với người sử dụng API đang debug và nhận được code print out data từ API - nó sẽ dễ dàng để đọc hơn. Hoặc nếu người sử dụng muốn lấy vài URL từ code của họ và cho vào browser - kết quả được in ra sẽ rất dễ dàng để đọc. Những điều này quá là nhỏ nhặt - nhưng đủ để làm cho một API dễ sử dụng - tích hợp.

** Còn về các dữ liệu thừa transfer thêm thì sao ? ** Hãy xem ví dụ thực tế bên dưới. Chúng ta sẽ kéo thử dữ liệu từ API của GitHub - đang sử dụng pretty print default.

$ curl https://api.github.com/users/veesahni > with-whitespace.txt
$ ruby -r json -e 'puts JSON JSON.parse(STDIN.read)' < with-whitespace.txt > without-whitespace.txt
$ gzip -c with-whitespace.txt > with-whitespace.txt.gz
$ gzip -c without-whitespace.txt > without-whitespace.txt.gz

Size out sẽ như sau :

thout-whitespace.txt - 1252 bytes
with-whitespace.txt - 1369 bytes
without-whitespace.txt.gz - 496 bytes
with-whitespace.txt.gz - 509 bytes

Ở ví dụ này, khoảng trắng tăng kích thước của output lên khoảng 8.5% đối với trường hợp ko dùng gzip và chỉ 2.6% nếu dùng gzip. Mặt khác, việc sử dụng gzip tiết kiệm được 60% bandwidth. Rõ ràng cost của việc pretty print khá nhỏ, cho nên hãy đảm bảo việc pretty print được hỗ trợ default và tất nhiên phải có gzip.

Thêm một số thông tin, Twitter gần đây cho biết rằng họ tiết kiệm được khoảng 80% ( trong 1 số trường hợp ) bandwidth khi enable gzip trên Streaming API.

Đừng sử dụng default envelope
Nhiều API trả về được wrap response như sau :

{
"data" : {
"id" : 123,
"name" : "John"
}
}

Việc này cho phép khá dễ dàng để include các metadata khác or các thông tin pagination, một vài client REST ko cho phép dễ dàng truy cập tới HTTP headers & JSONP request không có quyền truy cập tới các HTTP header. Tuy nhiên, với các chuanar đang được nhanh chóng áp dụng - thông qua là CORS và link header từ RFC 5988, enveloping bắt đầu trở nên ko cần thiết.

Chúng ta có thể giải phóng việc envelop này và chỉ cho vào khi cần thiết.

** Những case nào cần envelop API **

Có 2 trường hợp - nếu API cần hỗ trợ cross domain request thông qua JSONP hoặc nếu client không thể làm việc với HTTP header.

JSONP request đi kèm với một param query thêm ( thường tên là callback hoặc jsonp ) đại diện cho tên của hàm callback. Nếu có param này, API nên switch sang envelope mode - nơi mà nó luôn trả về 200 HTTP status và pass status code trong JSON payload. Bất kì một HTTP header thêm nào cũng có thể được gửi kèm với response và nên được map với JSON fields :

callback_function({
status_code: 200,
next_page: "https://..",
response: {
... actual JSON response body ...
}
})

Tương tự, để hỗ trợ một số client bị hạn chế về HTTP, cho phép một param đặc biệt ?envelope=true để trigger mode envelop ( ko cần chức năng JSONP callback).

JSON encoded vào POST, PUT & PATCH body
Nếu bạn đang theo đuổi cách tiếp cận trong bài viết này, sau đó bạn đã chấp nhận JSON cho các output API. Hãy xem xét JSON cho đầu vào API.

Nhiều API sử dụng mã hoá URL trong các request body API. Encode URL chính xác như tên của nó - request body nơi các cặng key value được encode sử dụng cùng một conventions giống như cái được sử dung để encode data trong URL query param. Việc này khá đơn giản, được hỗ trợ rộng rãi.

Tuy nhiên, encode URL có một số vấn đề khiến cho nó khó hiểu. Nó không có khái niệm về các kiểu dữ liệu. Điều này buộc API phải phân tích các số nguyên và boolean ra khỏi các string. Hơn nữa, nó không có khái niệm thực sự của cấu trúc phân cấp. Mặc dù có một số qui ước có thể xây dựng một số cấu trúc trong cặp giá trị quan trọng (như nối [ ] với một khoá để biểu diễn một mảng), tuy nhiên việc này chẳng thể so sánh được với cấu trúc phân cấp của JSON.

Nếu API đơn giản, mã hóa URL là đủ. Tuy nhiên, các API phức tạp phải gắn với JSON cho input API của chúng. Dù bằng cách nào, chọn một và nhất quán trên tất cả các API.

Một API chấp nhận các request POST, PUT & PATCH được JSON encode cũng cần yêu cầu phải đặt header Content-Type là application/json hoặc trả về mã 415 Unsupported Media Type HTTP.

Phân trang
Bạn có thể sử dụng envelope APIs cho việc include các dữ liệu phân trang trong envelope. Tuy nhiên, có nhiều sự lựa chọn tốt hơn. Cách chuẩn nhất hiện tại là include pagination details sử dụng Link header trong RFC 5988.

Một API sử dụng Link header có thể trả về một set các link đã được tạo do đó người sử dụng API ko cần build các link đó. Nó thực sự rất quan trọng nếu pagination dựa trên con trỏ. Đây là một ví dụ về Link header được sử dụng trong tài liệu của GitHub :

Link: <https://api.github.com/user/repos?page=3&per_page=100>; rel="next", <https://api.github.com/user/repos?page=50&per_page=100>; rel="last"

Tuy nhiên đây không phải là một giải pháp hoàn chỉnh vì nhiều APIs muốn trả lại các thông tin phân trang bổ sung, ví dụ như tổng số kết quả có sẵn. Một API yêu cầu gửi một số liệu count có thể custome HTTP header như X-Total Count.

Tự động tải các tài nguyên liên quan
Có nhiều trường hợp người dùng API cần tải dữ liệu liên quan đến (hoặc được tham chiếu) từ tài nguyên đang được yêu cầu. Thay vì bắt người sử dụng gọi API nhiều lần để biết thông tin này, sẽ có lợi ích đáng kể từ việc cho phép dữ liệu liên quan được trả lại và load cùng với tài nguyên ban đầu theo yêu cầu.

Tuy nhiên, vì điều này đi ngược lại một số nguyên tắc RESTful, chúng ta có thể giảm thiểu độ sai lệch nguyên tắc đó bằng cách chỉ làm như vậy dựa trên param query embed (hoặc expand).

Trong trường hợp này, query param embed sẽ là một danh sách các trường được cách ly bằng dấu phẩy. Ký hiệu dạng chấm có thể được sử dụng để chỉ các trường con. Ví dụ:

GET /tickets/12?embed=customer.name,assigned_user

Request trên sẽ trả về thông tin bổ sung thêm như thế này :
```json
{
"id" : 12,
"subject" : "I have a question!",
"summary" : "Hi, ....",
"customer" : {
"name" : "Bob"
},
assigned_user: {
"id" : 42,
"name" : "Jim",
}
}
```

Overriding the HTTP method
Một số client HTTP chỉ có thể làm việc với các yêu cầu GET và POST đơn giản. Để tăng khả năng tiếp cận cho các máy client hạn chế này, API cần một cách để ghi đè phương thức HTTP. Mặc dù không có bất kỳ tiêu chuẩn nào ở đây, quy ước phổ biến là chấp nhận tiêu đề yêu cầu X-HTTP-Method-Override với một string value có chứa một trong PUT, PATCH hoặc DELETE.

Lưu ý rằng override heaeder chỉ nên được chấp nhận khi request POST. GET yêu cầu không bao giờ thay đổi dữ liệu trên máy chủ!

Rate limiting

Để ngăn chặn sự lạm dụng, đây là một chuẩn nên được add vào API cho phép giới hạn tỷ lệ nhaats định. RFC 6585 cung cấp status code 429 Too Many Requests để đáp ứng yêu cầu này.

Tuy nhiên, có thể rất hữu ích để thông báo cho người tiêu dùng về các giới hạn của họ trước khi người sử dụng chạm đến giới hạn. Đây là một khu vực hiện nay thiếu nhiều tiêu chuẩn nhưng có một số conventions phổ biến sử dụng các trong response header HTTP.

Ít nhất, hãy bao gồm các header sau (sử dụng quy ước đặt tên của Twitter dưới dạng tiêu đề thường không có từ viết hoa giữa):

X-Rate-Limit-Limit - Lượng request cho phép tại thời điểm hiện tại
X-Rate-Limit-Remaining - Lương reqeust cho phép còn lại tại thời điểm hiện tại
X-Rate-Limit-Reset - Thời gian còn lại tại thời điểm hiện tại
Tại sao lại cần phải có thời gian sử dụng còn lại ? Timestamp chứa rất nhiều thông tin hữu ích nhưng ko cần thiết nư ngày - múi giờ. Một người sử dụng API muốn biết khi nào cần phải gửi lại request và số lượng giây còn lại để gửi với câu hỏi này sẽ là câu trả lại chuẩn cho người sử dụng. Nó cũng tránh việc không đồng bộ đồng hồ.

Một vài API sử dụng UNIX timestamp thay vì X-Rate-Limit-Reset. Đừng làm điều này !

Tại sao ko nên dùng UNIX timestamp thay cho X-Rate-Limit-Reset

Thông số HTTP đã được chỉ định sử dụng các định dạng ngày tháng của RFC 1123 (hiện đang được sử dụng trong header HTTP Date, If-Modified-Since & Last-Modified). Nếu chúng ta chỉ định một tiêu đề HTTP mới có dấu thời gian của một số loại khác, nó nên theo các conventions của RFC 1123 thay vì sử dụng timestamp UNIX.

Authentication
Một RESTful API nên stateless. Điều này có nghĩa là yêu cầu xác thực không nên phụ thuộc vào cookie hoặc session. Thay vào đó, mỗi request phải có một số chứng chỉ xác thực.

Bằng cách luôn sử dụng SSL, chứng chỉ xác thực có thể được đơn giản hóa thành một mã thông báo truy cập được tạo ngẫu nhiên và được phân phối trong trường user name của HTTP Basic Auth. Điều tuyệt vời là nó hoàn toàn browser explorable - trình duyệt sẽ chỉ nhắc nhở yêu cầu thông tin xác thực nếu nó nhận được mã 401 từ máy chủ.

Tuy nhiên, phương thức xác thực auth token-over-basic-auth này chỉ chấp nhận được trong những trường hợp thực tế để người dùng sao chép token từ một interface quản lý setting tới môi trường tích hợp API. Trong trường hợp không thể thực hiện được việc này, OAuth 2 sẽ được sử dụng để cung cấp token an toàn cho bên thứ ba. OAuth 2 sử dụng thẻ Bearer và cũng phụ thuộc vào SSL cho việc vận chuyển dữ liệu token.

API cần hỗ trợ JSONP sẽ cần phương pháp xác thực thứ ba request JSONP không thể gửi thông tin xác thực quyền truy cập HTTP Basic Auth credentials hoặc Bearer tokens. Trong trường hợp này, một param query đặc biệt access_token có thể được sử dụng. Lưu ý: Có vấn đề bảo mật vốn có khi sử dụng param query cho token vì hầu hết các máy chủ web lưu trữ các thông số truy cập trong server logs.

Caching
HTTP cung cấp một hệ thống caching built-in! Tất cả những gì bạn phải làm là include một số header khi response và thực hiện một số validation khi bạn nhận các thông tin từ request header.

Có 2 cách tiếp cận: ETag và Last-Modified

ETag: Khi tạo request, hãy include header HTTP ETag có chứa hash hoặc checksum của thực thể. Giá trị này sẽ thay đổi bất cứ khi nào output thực thể thay đổi. Bây giờ, nếu yêu cầu HTTP gửi đến có chứa tiêu đề If-None-Match với giá trị ETag tương ứng, API sẽ trả về mã trạng thái 304 Not Modified thay vì biểu hiện đầu ra của tài nguyên.

Last-Modified: Về cơ bản hoạt động như ETag, ngoại trừ việc nó sử dụng timestamps. Response Header Last-Modified chứa timestamp ở định dạng RFC 1123 được xác nhận hợp lệ đối với If-Modified-Since. Lưu ý rằng thông số HTTP đã có 3 định dạng ngày khác nhau và máy chủ cần được chuẩn bị để xử lý bất kỳ một trong số chúng.

Errors
Giống như trang lỗi HTML hiển thị thông báo lỗi cho người truy cập, một API nên cung cấp một thông báo lỗi hữu ích. Sự trình bày biểu diễn của một lỗi không nên khác của bất kỳ tài nguyên nào.

API nên luôn trả về mã trạng thái HTTP. Lỗi API thường được chia thành 2 loại: mã trạng thái series 400 cho các sự cố của client và series 500 cho các sự cố của máy chủ. Ít nhất, API phải chuẩn hóa rằng tất cả các mã lỗi 4xx đi kèm với JSON. Cơ thể lỗi của JSON cần cung cấp một vài điều cho nhà phát triển - thông báo mesage lỗi hữu ích, mã lỗi duy nhất (có thể được tìm kiếm để biết thêm trong tài liệu) và có thể là mô tả chi tiết. Đại loại như sau :
```json
{
"code" : 1234,
"message" : "Something bad happened :(",
"description" : "More details about the error here"
}

Xác nhận lỗi cho các yêu cầu PUT, PATCH và POST sẽ cần breakdown field. Đây là mô hình tốt nhất bằng cách sử dụng mã lỗi cấp cao nhất cho các lỗi xác thực và cung cấp các lỗi chi tiết trong trường lỗi bổ sung, như sau:

{
"code" : 1024,
"message" : "Validation Failed",
"errors" : [
{
"code" : 5432,
"field" : "first_name",
"message" : "First name cannot have fancy characters"
},
{
"code" : 5622,
"field" : "password",
"message" : "Password cannot be blank"
}
]
}

```
HTTP status codes
HTTP định nghĩa một nhóm các mã lỗi để có thể dùng trong response API. Dưới đây là danh sách những mã lỗi mà bạn sẽ sử dụng :

200 OK - Trả về thành công cho các request GET, PUT, PATCH hoặc DELETE. Cũng có thể sử dụng cho POST
201 Created - Trả về cho POST trong trường hợp tạo mới. Nên được kết hợp với Location header để chỉ định tài nguyên mới
204 No Content - Trả về thành công cho một request nhưng ko có body (ví dụ DELETE request)
304 Not Modified - Khi sử dụng HTTP caching headers
400 Bad Request - Yêu cầu không đúng định dạng
401 Unauthorized - Xác thực không hợp lệ.
403 Forbidden - Xác thực thành công nhưng user không có quyền truy cập tài nguyên
404 Not Found - Tài nguyên không tồng tại
405 Method Not Allowed - Khi một method HTTP được request nhưng ko cho phép tới user đã xác thực
410 Gone - Tài nguyên ở endpoint không còn tồn tại.
415 Unsupported Media Type - Content type không hợp lệ
422 Unprocessable Entity - Sử dụng cho các lỗi validation
429 Too Many Requests - Request bị reject do giới hạn rate limiting
