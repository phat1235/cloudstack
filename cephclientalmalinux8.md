# ✅ CÁCH FIX ĐÚNG (AlmaLinux 8 + Ceph client)

## 🔥 Bước 1: XÓA repo sai

```bash id="rm1"
rm -f /etc/yum.repos.d/ceph.repo
```

---

## 🔥 Bước 2: Tạo repo đúng (WORKING)

### 👉 Dùng repo chính thức mới:

```bash id="repo1"
cat > /etc/yum.repos.d/ceph.repo <<EOF
[ceph]
name=Ceph packages
baseurl=https://download.ceph.com/rpm-18.2.2/el8/\$basearch
enabled=1
gpgcheck=1
gpgkey=https://download.ceph.com/keys/release.asc
EOF
```

👉 `18.2.2 = Reef (stable client compatible)`

---

## 🔥 Bước 3: Clean + rebuild cache

```bash id="cache1"
dnf clean all
dnf makecache
```

---

## 🔥 Bước 4: Install Ceph client

```bash id="install1"
dnf install -y ceph-common ceph-fuse
```

---

# ✅ Kiểm tra

```bash id="check1"
ceph -v
ceph-fuse --version
```




