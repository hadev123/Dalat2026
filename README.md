Vue:
VUE khác với Nuxt.js: VUE là CSR, NuxtJS là SSR. File của Nuxt.js được tạo sẵn hết (Vue 2, Vue-router, VueX, …) không cần import. 


SPA là một kiểu lập trình web mà ở đó người dùng có thể truy cập vào nhiều trang web con khác nhau mà không làm ảnh hưởng đến trang web gốc. Khi người dùng truy cập vào bất kỳ thành phần nào trên trang, SPA sẽ chỉ chạy nội dung của thành phần đó mà không tải lại toàn bộ trang như các web truyền thống. Các thành phần chung như header, footer, thanh menu sẽ được giữ nguyên.

DOM được dùng để truy xuất và thao tác trên các tài liệu có cấu trúc dạng HTML hay XML bằng các ngôn ngữ lập trình thông dụng như Javascript

Khi render, Vue so sánh Virtual DOM mới với cũ rồi chỉ cập nhật phần khác biệt vào DOM thật, giúp tăng hiệu năng.

4 giai đoạn ở vòng đời: 
Trong Vue 3, vòng đời component chia thành 3 giai đoạn chính: mounting, updating, unmounting. Khi khởi tạo thì chạy setup(),onBeforeMount() → gọi trước khi component gắn vào DOM, sau đó onMounted() để thao tác sau khi render. Khi dữ liệu thay đổi thì có onBeforeUpdate và onUpdated. Cuối cùng khi huỷ component thì có onBeforeUnmount và onUnmounted. Thường dùng nhất là onMounted để gọi API và onUnmounted để cleanup

Chi tiết https://viblo.asia/p/vuejs-vong-doi-cua-mot-vue-instance-lifecycle-hooks-Ljy5Vmazlra
Đây là Vue2
1. Giai đoạn khởi tạo: 
beforeCreate
created

2. Giai đoạn gắt kết DOM:
beforeMount 
mounted 

3. Giai đoạn cập nhật DOM khi dữ liệu thay đổi:
beforeUpdate 
updated 

4. Giai đoạn hủy instance
beforeDestroy 
destroyed 


Hooks là các hàm Javascript, nhưng nó bắt buộc thêm hai quy tắc: Chỉ gọi Hooks trên cùng. Không gọi Hooks bên trong vòng lặp, điều kiện, hoặc các hàm lồng nhau.

Keep - alive tag sử dụng để giữ trạng thái hiện có của component và nó tránh việc render lại component quá nhiều. Các đối tượng này đóng ở trong tag keep - alive sẽ giữ instances.

Dynamic route matching nó giúp chúng ta map tới các route với các pattern khác nhau.

Hàm data() luôn trả về 1 object

Có hai cách bind data để view trong VueJs: 
One-way data binding 
Two-way data binding

vue-class-component: tạo các component theo cú pháp class-style

v-slot: cho phép bạn đặt nội dụng ở một vị trí mới hoặc tạo ra những component chung, hoặc có thể chèn nội dung từ component cha vào component con 
(Component con sẽ được define trước vị trí thẻ slot, sau đó component cha chèn thêm vào đúng với cái tên mà component con đã đặt tên )
Scoped slots:  là một loại đặt biệt của slot giúp bạn có thể truyền dữ liệu từ component con lên component cha thông qua việc gán dữ liệu thông qua thuộc tính

Slot thường: parent chỉ truyền nội dung vào child.
Scoped slot: child truyền dữ liệu ra, parent quyết định hiển thị.


Lazy loading: là cách chúng ta thực hiện đầu tiên khi tối ưu tốc độ tải trang web hay ứng dụng Vuejs (chia tách code thành những phần nhỏ) hay dùng cho Dynamic import



Sự khác nhau giữa v-show và v-if:
Với v-show thì chỉ ẩn và hiện các thẻ HTML bằng CSS, còn v-if thì xóa và thêm.
v-show không sử dụng được với template, không kết hợp được với v-else và v-else-if.


Khi nào nên dùng v-if khi nào nên dùng v-show?
Đối với trường hợp dữ liệu thay đổi nhiêu trong một lần chạy thì bạn nên chọn v-show vì nó chỉ render lần đầu khi chạy.
Còn đối với dữ liệu không thay đổi trong 1 lần chạy thì lên chọn v-if vì nó có tính chất private hơn.


Tại sao dùng “key” trong v-for:
Trong Vue, key trong vòng v-for dùng để định danh duy nhất cho mỗi phần tử, giúp Vue cập nhật DOM hiệu quả và tránh lỗi khi thêm/xóa/sắp xếp. Thường dùng id thay vì index." - Chỉ render đúng item cần thay đổi thôi thay vì render lại cả danh sách
Mixins là cách gom logic chung (data, methods, computed, lifecycle hooks) vào một object rồi “trộn” vào nhiều component của vue2. Còn vue3 dùng Composable function  giống như common function, nhưng thay vì chỉ xử lý dữ liệu, nó còn có thể tạo và quản lý reactive state. Nhờ đó ta dễ dàng tái sử dụng logic giữa nhiều component.
watch cần truyền biến cụ thể để theo dõi, còn watchEffect thì không cần — nó tự động theo dõi tất cả biến reactive được dùng trong callback.
Trong watch:
immediate: true → Callback sẽ chạy ngay lần đầu khi khai báo watch, ngoài việc chạy khi giá trị thay đổi. → Hữu ích khi bạn muốn xử lý dữ liệu ban đầu (ví dụ: gọi API ngay khi component mount).
deep: true → Dùng khi theo dõi object hoặc array. → Vue sẽ theo dõi mọi thay đổi bên trong (nested property) chứ không chỉ theo dõi tham chiếu. → Nếu không có deep: true, thay đổi bên trong object/array sẽ không trigger callback.

Trong Vue 3, watch(immediate) và watchEffect đều chạy ngay trong setup, trước khi DOM render. Thứ tự log phụ thuộc vào vị trí khai báo trong code, còn onMounted thì luôn chạy sau khi DOM render xong


Sự khác nhau giữa computed và methods:
computed sẽ khác với methods ở chỗ computed được lưu vào cache và computed sẽ chỉ được thay đổi khi dữ liệu bên trong nó thay đổi. Còn methods không thể biết các giá trị trong hàm có thay đổi hay không nên hàm sẽ không chạy lại nếu các giá trị trong hàm đó thay đổi.
Sự khác nhau giữa created và mounted:
created được chạy khi data, event đã thiết lập thành công nhưng các thẻ trong template và DOM ảo vẫn chưa được render ra. Nếu bạn cố gắng truy cập vào các phần tử DOM trong hàm này thì nó sẽ báo lỗi. Nên trong created thường được sử dụng để gọi API và gán kết với các giá trị trong data.
mounted giai đoạn này, mounted hook sẽ cho phép chúng ta có thể truy cập vào phần tử trong DOM. Tức là khi này, DOM đã được gắn kết.

Props: + Dữ liệu đẩy từ component cha sang component con
	Có 2 cách:
	+ Dùng mảng tên các props
	+ Nhận object (dạng key: value)
Props giong nhu data (component cha khởi tạo props, component con lấy về)


Emit: chuyển data từ con sang cha


@submit.prevent trong form sẽ ko chuyển trang và đứng nguyên ở trang đấy

Filter trong Vue: dùng để biến đổi giá trị một biểu thức, ví dụ như biển đổi số thành dạng tiền tệ, dạng timestamp thành ngày, tháng, năm. Filter sẽ không làm thay đổi giá trị mà vẫn hiển thị theo dạng mình mong muốn

VueX:  là một kho quản lý dữ liệu tập trung (state management), giúp quản lý các state trong các components. Dùng VueX sẽ đơn giản hóa trong việc thay đổi, lấy dữ liệu. Tất cả các components đều có khả năng đến store để lấy data mà không cần phải emit. vuex cung cấp phần modules, giúp tách store lớn ra thành các modules nhỏ.


Có 4 thành phần chính: 
State: Là object chứa dữ liệu và chia sẻ cho toàn ứng dụng được
Getters: là những hàm để lấy dữ liệu state ra
Mặc định VueX getters chấp nhận 2 tham số: 
state: là state object của ứng dụng
getters: là store.getters object – tức là chúng ta có thể gọi getter của một store khác
Mutations: để thay đổi giá trị của state object. Mutations phải là synchronous (đồng bộ). Muốn lấy mutations vào component nào thì dùng commit 
Mutations cũng chấp nhận 2 tham số:
State: là state object của ứng dụng.
Payload: là giá trị bạn muốn truyền vào cho mutations
Actions: sẽ thường chứa logic liên quan đến nghiệp vụ business và các bạn nên hiểu là nó không trực tiếp thay đổi state. Nếu muốn thay đổi State thì các bạn cần dùng một Commit đã được định nghĩa tại Mutations. Lí do là bởi vì Actions thường được chạy bất đồng bộ (Code của bạn vẫn chạy khi mà actions chưa hoàn thành) và như vậy khi nó hoàn thành thì chúng ta mới lên Commit để change data.
Action sẽ truyền vào context (là trạng thái store ở hiện tại)


Lấy data từ state về component thì getter từ state ra (dùng mapGetter)
Muốn thay đổi data từ component về state thì trải qua 2 bước đó là Action và Mutation

Vue2 và Vue3: 
https://blog.tda.company/vue2-to-vue3-what-s-new/


Vue là binding dữ liệu 1 chiều, props chỉ đi từ cha -> con và con không được phép thay đổi trực tiếp props, nếu muốn thay đổi đổi ngược lại con -> cha thì dùng emit để báo cho cha có thay đổi và cha sẽ cập nhật lại state của mình rồi truyền xuống con props


Pinia thì có các bước sau:
1. Dùng defineStore để định nghĩa store
2. Tạo state dữ liệu reactive
3. Tạo getters: giống computed, tạo giá trị dẫn xuất từ state
4. Tạo actions: giống methods, thay đổi state hoặc xử lý logic


  Immutable = dữ liệu bất biến, không thể sửa trực tiếp.




