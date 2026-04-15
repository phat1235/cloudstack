
## Affinity và Anti-Affinity trong Apache CloudStack

Trong Apache CloudStack, **Host Affinity** và **Host Anti-Affinity** đề cập đến khả năng đảm bảo một cách xác định (deterministic) rằng một tập hợp các **Instance** sẽ chạy trên cùng một host hypervisor hoặc trên các host khác nhau, nhằm đáp ứng các yêu cầu workload cụ thể.

---

## Cách Affinity Groups hoạt động trước đây

Trước phiên bản CloudStack 4.18, có hai loại Affinity Group:

![](https://raw.githubusercontent.com/phat1235/cloudstack/2ab2f7209f522b32b251ff8c749d4dffe6b767bc/imgs/Affinity%20Groups/1-2.png)

### • Host Affinity

Host Affinity Group cho phép người dùng chỉ định rằng một tập hợp Instance phải luôn chạy trên cùng một host hypervisor.

Điều này giúp:

* Giảm độ trễ (latency) xuống mức thấp nhất
* Tăng băng thông tối đa giữa các Instance
  (vì traffic không cần rời khỏi hypervisor)

Tuy nhiên:

* Nếu host không đủ tài nguyên để chạy toàn bộ Instance trong group
  → việc deploy Instance sẽ **thất bại**

---

### • Host Anti-Affinity

Ngược lại, Host Anti-Affinity Group cho phép đảm bảo các Instance luôn chạy trên **các host khác nhau**.

Điều này giúp:

* Phân tán ứng dụng theo chiều ngang (horizontal scaling)
* Tăng khả năng sẵn sàng (availability) khi một host bị lỗi

Tuy nhiên:

* Nếu không có đủ host khác nhau với tài nguyên phù hợp
  → việc deploy Instance sẽ **thất bại**

---

## Giới thiệu Adaptive Affinity Groups (CloudStack 4.18)

**Adaptive Affinity Groups** là tính năng mới trong CloudStack 4.18, giúp tăng tính linh hoạt khi triển khai Instance.

![](https://raw.githubusercontent.com/phat1235/cloudstack/2ab2f7209f522b32b251ff8c749d4dffe6b767bc/imgs/Affinity%20Groups/2.png)

Điểm khác biệt chính:

* Các yêu cầu Affinity / Anti-Affinity được áp dụng theo kiểu **best-effort** (cố gắng tối đa)
* Việc deploy Instance **vẫn thành công** ngay cả khi không đủ tài nguyên để đáp ứng hoàn toàn yêu cầu

Các loại Affinity Group cũ vẫn tồn tại, nhưng được đổi tên thành:

* **Host Affinity (strict)**
* **Host Anti-Affinity (strict)**

---

## Các loại Non-Strict (linh hoạt)

### • Non-strict Host Affinity Group

* Instance sẽ được đặt cùng một host **nếu có thể**
* Nếu không đủ tài nguyên:
  → CloudStack vẫn deploy sang host khác

---

### • Non-strict Host Anti-Affinity Group

* Instance sẽ được phân tán trên nhiều host **nếu có thể**
* Nếu không đủ tài nguyên:
  → vẫn có thể deploy lên cùng host

---

## Cách CloudStack chọn Host (Strict vs Non-Strict)

Trước phiên bản 4.18:

* Chỉ có **Strict Affinity**
* Nếu không thỏa điều kiện → deploy thất bại
![](https://raw.githubusercontent.com/phat1235/cloudstack/2ab2f7209f522b32b251ff8c749d4dffe6b767bc/imgs/Affinity%20Groups/Picture-3.png)

Sau 4.18:

* Có thể dùng **Non-Strict**
* Nếu không thỏa điều kiện:
  → CloudStack sẽ deploy như bình thường (không thuộc Affinity Group)
  → sử dụng thuật toán `vm.allocation.algorithm`

![](https://raw.githubusercontent.com/phat1235/cloudstack/2ab2f7209f522b32b251ff8c749d4dffe6b767bc/imgs/Affinity%20Groups/Picture-4.png)
---

## Cách tính ưu tiên Host (Host Priority)

Với Non-Strict Affinity Groups, CloudStack sử dụng **priority (độ ưu tiên)** để chọn host.

* Mặc định: priority = 0
* Nếu host có Instance cùng nhóm Anti-Affinity:
  → priority giảm

Sau đó, các host sẽ được sắp xếp lại theo priority.

---

### Ví dụ 1: Non-Strict Anti-Affinity

* Host-1 có 2 Instance → priority = -2
* Host-2 có 3 Instance → priority = -3

→ Chọn Host-1 (vì -2 > -3)

---

### Ví dụ 2: Non-Strict Affinity

* Host-1 có 2 Instance → priority = 2
* Host-2 có 3 Instance → priority = 3

→ Chọn Host-2 (vì 3 > 2)

---

### Ví dụ 3: Kết hợp cả Affinity và Anti-Affinity

Host-1 có:

* 2 Instance (Affinity)
* 3 Instance (Anti-Affinity)

Cách tính:

```
0 (mặc định)
+ 2 (Affinity)
- 3 (Anti-Affinity)
= -1
```

---

## Kết luận

Với Adaptive Affinity Groups trong Apache CloudStack 4.18, việc triển khai Instance trở nên linh hoạt hơn rất nhiều. Người dùng có thể tối ưu cách phân bố Instance để phù hợp hơn với yêu cầu workload của ứng dụng, mà không còn bị giới hạn bởi các điều kiện cứng như trước đây.
