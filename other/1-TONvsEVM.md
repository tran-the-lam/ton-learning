# Hợp đồng thông minh của bạn cần trả tiền thuê và tính phí cho người dùng

Blockchain như một kho lưu trữ dữ liệu bất biến và vĩnh cửu, là một khái niệm tuyệt vời trên giấy tờ, nhưng như chúng ta sẽ sớm thấy, nó khá phi thực tế để mở rộng quy mô. Mô hình phí của Ethereum được lấy cảm hứng từ mô hình ngân hàng. Bạn muốn gửi một số tiền, bạn phải trả cho ngân hàng một khoản phí giao dịch. Ai chịu trách nhiệm thanh toán phí? Người dùng đã bắt đầu chuyển.

Còn việc lưu trữ dữ liệu trên blockchain - ví dụ như triển khai mã byte cho hợp đồng thông minh mới thì sao? Mô hình Ethereum quy định rằng người gửi giao dịch triển khai sẽ phải trả phí. Tuy nhiên, khoản phí này chỉ được trả một lần, tuy nhiên nếu dữ liệu trên chuỗi là vĩnh viễn, các thợ mỏ sẽ phải tiếp tục trả chi phí cơ sở hạ tầng để giữ lại dữ liệu này trong nhiều năm tới. Các tính kinh tế về phí này không cộng lại và nếu bạn cố gắng mở rộng quy mô cho hàng tỷ người dùng, cuối cùng chúng sẽ sụp đổ.


### Chuyển từ ngân hàng sang tin nhắn tức thời
Mô hình phí trên TON khá khác biệt. Thay vì mô phỏng tài khoản ngân hàng, TON được lấy cảm hứng từ các ứng dụng web như * tin nhắn tức thời*. Ai là người trả chi phí gửi tin nhắn trên Facebook Messenger? Đó chắc chắn không phải là người bắt đầu chuyển tiền. Nhà phát triển ứng dụng, Facebook Inc (hoặc Meta Inc, tôi không theo dõi, tôi sử dụng Telegram), thực sự đang chi trả các chi phí và Facebook Inc có trách nhiệm thu hồi các chi phí này bằng cách nào đó và tự cấp vốn.

Theo đó, trong TON, bản thân dapp cần phải trả chi phí tài nguyên của chính mình. Mỗi hợp đồng thông minh đều có số dư token TON và sử dụng số dư này để trả tiền thuê nhà. Nếu hợp đồng thông minh hết tiền, cuối cùng nó sẽ bị xóa (đừng lo lắng, mọi thứ đều có thể phục hồi được). Lưu ý rằng việc thanh toán cho chuỗi lưu trữ không diễn ra một lần mà việc thanh toán tiền thuê là liên tục. Nếu bạn chỉ giữ dữ liệu trong một khoảng thời gian ngắn, bạn sẽ phải trả ít hơn đáng kể. Tính kinh tế về phí này phù hợp hơn với chi phí của người khai thác và do đó dễ dàng mở rộng quy mô hơn.

Rất giống với Facebook Inc, nhà phát triển hợp đồng ở TON có rất nhiều quyền tự do lựa chọn cách cấp vốn cho hoạt động của mình. Nhà phát triển có thể tự bỏ tiền túi tài trợ cho hợp đồng bằng mã thông báo TON và trợ cấp cho người dùng; hoặc nó có thể tính phí gas từ người dùng cho các hành động khác nhau và giữ lượng gas này ở mức cân bằng để thanh toán tiền thuê trong tương lai.


# Các cuộc gọi giữa các hợp đồng thông minh không đồng bộ và không nguyên tử
Một trong những yếu tố hỗ trợ tuyệt vời cho hệ sinh thái DeFi mạnh mẽ trên Ethereum là khả năng kết hợp liền mạch của các hợp đồng. Trong một giao dịch duy nhất, bạn có thể lấy một số WBTC, cung cấp nó làm tài sản thế chấp cho hợp đồng của Hợp chất và sử dụng nó để vay USDC, giao dịch USDC này với hợp đồng của Uniswap để có thêm WBTC - và do đó tận dụng vị thế WBTC của bạn. Toàn bộ quá trình thậm chí còn đơn giản - nếu bất kỳ bước nào trong số này không thành công, thậm chí là bước cuối cùng, toàn bộ giao dịch sẽ quay trở lại như chưa từng xảy ra.

Khi hợp đồng thông minh của bạn gọi một phương thức của hợp đồng thông minh khác, cuộc gọi sẽ được xử lý ngay lập tức trong cùng một giao dịch. Ethereum về mặt này rất giống với việc chạy toàn bộ phần phụ trợ của bạn trên một máy chủ. Mọi phần trong chương trình phụ trợ của bạn sẽ có thể truy cập đồng bộ vào mọi phần khác - một cách tiếp cận rất dễ hiểu. Nó chỉ có một điều lưu ý là nó chỉ có thể phát triển miễn là nó vừa với một chỗ.

### Moving from a single server to a cluster of microservices
Nếu bạn tưởng tượng Ethereum như một khối nguyên khối trên một máy chủ thì TON giống với một cụm các dịch vụ vi mô hơn. Hãy nghĩ rằng mọi hợp đồng thông minh có thể đang chạy trên một máy khác nhau. Nếu hai hợp đồng thông minh muốn gọi cho nhau, giống như hai microservice đang giao tiếp, chúng có thể gửi tin nhắn qua mạng. Tin nhắn này mất một thời gian để truyền đi, vì vậy việc liên lạc đột nhiên không đồng bộ! Điều này có nghĩa là khi hợp đồng thông minh của bạn gọi một phương thức của hợp đồng thông minh khác, cuộc gọi sẽ được xử lý sau khi giao dịch kết thúc, trên một số khối tương lai khác.

Lý do này khó hơn nhiều. Điều gì xảy ra nếu các điều kiện thay đổi kể từ khi tin nhắn được gửi cho đến khi nó được nhận? Ví dụ: số dư hợp đồng cuộc gọi có một giá trị, nhưng vào thời điểm hợp đồng thứ hai xử lý cuộc gọi, số dư đã thay đổi. Việc duy trì tính nhất quán khó khăn hơn và lỗi có thể gia tăng. Còn tính nguyên tử thì sao? Điều gì xảy ra nếu bạn gọi ba cuộc gọi và chỉ cuộc gọi cuối cùng không thành công? Nếu bạn cần khôi phục tất cả các thay đổi, bạn sẽ phải thực hiện thủ công.


# Hợp đồng thông minh của bạn không thể chạy phương thức getter trên các hợp đồng khác
Đây thực sự là một diện mạo khác của mục trước đó trong danh sách. Trên Ethereum, nơi các lệnh gọi giữa các hợp đồng được đồng bộ hóa, việc đọc dữ liệu từ một hợp đồng thông minh khác rất đơn giản. Giả sử hợp đồng của tôi có số dư USDC. Vì USDC cũng là một hợp đồng nên để biết số dư của chính nó, hợp đồng của tôi sẽ phải gọi phương thức getBalance của hợp đồng USDC.

Bạn có nhớ nguyên khối chạy trên một máy chủ không? Một trong những lợi ích lớn nhất của phương pháp này là mọi dịch vụ đều có thể đọc trực tiếp bộ nhớ trạng thái của mọi dịch vụ khác.

### Moving from a single server to a cluster of microservices
Khi chúng ta có các vi dịch vụ riêng biệt chạy trên các máy khác nhau, việc đọc bộ nhớ trạng thái trên các dịch vụ đột nhiên là không thể. Hợp đồng thông minh trên TON chỉ có thể giao tiếp bằng cách gửi tin nhắn không đồng bộ. Nếu bạn cần truy vấn dữ liệu từ một hợp đồng khác và yêu cầu câu trả lời ngay lập tức thì bạn đã không gặp may.

Nó thực sự thậm chí còn xa lạ hơn. Nếu bạn thấy các phương thức getter trên hợp đồng thông minh TON, chẳng hạn như getBalance - những phương thức này không thể truy cập được từ các hợp đồng thông minh khác. Các phương thức Getter chỉ có thể được gọi bởi các máy khách ngoài chuỗi, tương tự như cách ví Ethereum của bạn có thể sử dụng một nút đầy đủ như Infura để truy vấn bất kỳ trạng thái hợp đồng thông minh nào.

# Mã hợp đồng thông minh không phải là bất biến và có thể dễ dàng sửa đổi
Nguồn cảm hứng ban đầu cho dapp trên Ethereum là các tài liệu pháp lý do luật sư soạn thảo - do đó có tên là 'hợp đồng thông minh'. Nhà phát triển lập trình các điều khoản của hợp đồng pháp lý dưới dạng mã và mã, như bạn biết, là luật. Khi hai bên trong thế giới thực ký hợp đồng, hợp đồng đó là bất biến. Nếu bất kỳ bên nào muốn thay đổi các điều khoản của hợp đồng thì thay vào đó họ sẽ soạn thảo một hợp đồng mới.

Đúng như cách tiếp cận này, mã của hợp đồng thông minh trên Ethereum được thiết kế để không thay đổi và không bao giờ được sửa đổi. Trong những năm qua, cộng đồng nhà phát triển đã học cách khắc phục hạn chế này và tạo ra một số mô hình phức tạp dựa vào các thủ thuật như hợp đồng proxy trỏ đến một hợp đồng khác để triển khai nâng cấp.

### Chuyển từ luật sư sang kỹ sư phần mềm
Không giống như luật sư, các kỹ sư phần mềm được dạy rằng mọi đoạn mã đều có lỗi trong đó. Và ngay cả khi sai sót không bao giờ xảy ra, các yêu cầu vẫn thay đổi theo thời gian và mã thường phải được nâng cấp và sửa đổi.

Theo TON, giả định rằng hợp đồng là bất biến sẽ bị loại bỏ hoàn toàn. Hợp đồng thông minh có thể tự do sửa đổi mã của riêng mình giống như ghi vào bất kỳ biến trạng thái nào khác. Nếu một hợp đồng ghi vào biến mã thì nó có thể thay đổi được và nếu không thì nó sẽ không thay đổi được. Đây không phải là một thay đổi lớn trong thực tế, nó chỉ làm cho mẫu proxy rườm rà trở nên dư thừa.


# Bạn không nên có cấu trúc dữ liệu không giới hạn ở trạng thái hợp đồng của mình
Đây là một vấn đề phức tạp cần mất một chút thời gian để hiểu nhưng sẽ giải thích lý do tại sao một số hợp đồng thông minh trên TON được thiết kế theo cách hiện tại.

Cấu trúc dữ liệu không giới hạn là các biến trạng thái trong hợp đồng thông minh có thể phát triển vô thời hạn. Hãy xem xét hợp đồng ERC20 triển khai mã thông báo USDC. Hợp đồng này cần duy trì bản đồ số dư trên mỗi địa chỉ người dùng. Số lượng người nắm giữ USDC khác nhau có thể tăng vô thời hạn vì USDC có thể được đúc với số lượng lớn và chia thành từng phần nhỏ. Nói cách khác, số lượng phím trên bản đồ có thể nhiều như bạn muốn.

Điều gì xảy ra nếu kẻ tấn công cố gắng spam hợp đồng bằng cách thêm ngày càng nhiều mục? Liệu họ có thể gây ra một số cuộc tấn công DoS và ngăn cản những người dùng trung thực khác sử dụng hợp đồng này không? Ethereum giải quyết vấn đề này khá dễ dàng cho các nhà phát triển hợp đồng thông minh. Mô hình phí Ethereum quy định rằng người dùng ghi dữ liệu trạng thái mới sẽ phải trả phí cho dữ liệu này. Điều này có nghĩa là kẻ tấn công của chúng tôi sẽ phải trả giá đắt cho thư rác của họ. Ngoài ra, chi phí gas để ghi vào bản đồ trên Ethereum là không đổi và không phụ thuộc vào lượng dữ liệu mà bản đồ này chứa, điều đó có nghĩa là những người dùng khác sẽ không bị spam. Điểm mấu chốt là việc gửi thư rác bản đồ trên Ethereum là không kinh tế và hệ thống cung cấp sự bảo vệ.

### Chuyển từ bản đồ không giới hạn sang hợp đồng không giới hạn
Thật không may cho các nhà phát triển hợp đồng thông minh TON, hệ thống không bảo vệ khỏi việc gửi thư rác các cấu trúc dữ liệu không giới hạn ở trạng thái hợp đồng. Mô hình phí gas TON chỉ ra rằng chi phí ghi không cố định, chi phí thường tỷ lệ thuận với lượng dữ liệu tồn tại trong cấu trúc dữ liệu. Hành vi này bắt nguồn từ sự phụ thuộc của TON vào kiến ​​trúc 'Túi di động' - trạng thái hợp đồng được chia thành các khối 1023 bit được gọi là 'ô' mà nhà phát triển bắt buộc phải duy trì. Bản đồ được triển khai dưới dạng cây gồm các ô và việc ghi vào một chiếc lá trên cây yêu cầu phải viết các giá trị băm mới dọc theo toàn bộ chiều cao của nó. Nếu kẻ tấn công spam các khóa trên bản đồ, một số số dư của người dùng sẽ bị đẩy xuống thấp đến mức việc cập nhật chúng sẽ vượt quá giới hạn gas.

Do đó, cách tốt nhất trong TON là tránh các cấu trúc dữ liệu không bị ràng buộc ở trạng thái. Điều này sẽ bảo vệ hợp đồng khỏi các lỗ hổng DoS xảo quyệt. Chủ đề này có lẽ xứng đáng có một bài đăng blog độc lập, nhưng giải pháp tóm lại là dựa vào việc bảo vệ hợp đồng. Nếu chúng ta có số lượng số dư người dùng tiềm năng là vô hạn trong hợp đồng USDC của mình, thì chúng ta nên chia hợp đồng đơn lẻ thành nhiều hợp đồng con - mỗi hợp đồng con giữ số dư cho một người dùng.

Điều này giải thích tại sao hợp đồng thu thập NFT trên TON đặt mọi mặt hàng vào hợp đồng riêng của nó (số lượng mặt hàng có thể không bị giới hạn); và tại sao các hợp đồng mã thông báo có thể thay thế trên TON lại đặt số dư của mỗi người dùng vào hợp đồng riêng của họ.

Chúng tôi thường cung cấp một chút lý do tại sao TON được thiết kế theo cách này. Mô hình phí gas Ethereum trong đó việc ghi bản đồ là cố định và không phụ thuộc vào kích thước bản đồ đã được đơn giản hóa quá mức. Trên thực tế, khi kích thước bản đồ tăng lên, người khai thác cần nhiều nỗ lực hơn để thay đổi nội dung của chúng. Nỗ lực thêm này là không đáng kể miễn là bản đồ còn nhỏ, nhưng khi bản đồ có thể tăng lên hàng tỷ mục thì điều này không còn xảy ra nữa.

# Ví là hợp đồng và một khóa công khai có thể triển khai nhiều ví

Trên Ethereum, ví của người dùng đồng nghĩa với địa chỉ của họ và địa chỉ được lấy trực tiếp từ khóa chung (và khóa riêng tương ứng của nó). Đây là mối quan hệ 1:1, có một địa chỉ cho mỗi khóa chung và một khóa chung cho mỗi địa chỉ. Miễn là người dùng biết khóa riêng của mình, họ sẽ không bao giờ bị mất ví.

Ngoài ra, người dùng trên Ethereum không cần phải làm gì đặc biệt để có ví. Địa chỉ Ethereum là ví. Địa chỉ có thể chứa đồng tiền gốc ETH, địa chỉ có thể chứa mã thông báo ERC20 và NFT, đồng thời địa chỉ có thể gửi và ký giao dịch trực tiếp với các hợp đồng thông minh khác.

### Moving from address to contract

Trên TON, ví không được ngụ ý, chúng là các hợp đồng thông minh độc lập phải được triển khai giống như bất kỳ hợp đồng thông minh nào khác. Khi người dùng mới muốn bắt đầu sử dụng chuỗi khối TON, bước đầu tiên của họ sẽ là triển khai ví trên chuỗi. Địa chỉ của ví này được lấy từ mã hợp đồng ví và các tham số init khác nhau như khóa chung của người dùng.

Điều này có nghĩa là người dùng có thể triển khai nhiều ví, mỗi ví có địa chỉ riêng. Các ví có thể khác nhau về mã của chúng (các phiên bản mã chính thức khác nhau được tổ chức xuất bản tùy từng thời điểm) hoặc về các tham số init của chúng (một trong những tham số này thường là số thứ tự). Điều này cũng có nghĩa là người dùng biết khóa riêng của họ vẫn phải cố gắng ghi nhớ địa chỉ ví của họ (hoặc các tham số init được sử dụng trong cấu trúc của nó).

Gửi giao dịch tới một số dapp trên TON liên quan đến việc ký tin nhắn bằng khóa riêng của người dùng. Không giống như Ethereum, giao dịch này không được gửi đến hợp đồng thông minh dapp mà đến hợp đồng ví của người dùng, hợp đồng này sẽ chuyển tiếp tin nhắn đến hợp đồng thông minh dapp.

Phương pháp thiết kế này mở ra một chiều hướng linh hoạt mới trên TON. Các hợp đồng ví mới có thể được cộng đồng phát minh theo thời gian, ví dụ: hãy xem xét một ví không có số thứ tự (số thứ tự giao dịch) cho phép nhiều giao dịch được gửi song song từ các khách hàng khác nhau mà không cần đồng bộ hóa trước. Ngoài ra, các ví đặc biệt như ví đa chữ ký (cũng trên Ethereum yêu cầu triển khai hợp đồng thông minh đặc biệt), hoạt động giống như các đối tác thông thường của chúng.