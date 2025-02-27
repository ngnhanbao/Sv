using System;

namespace QLSinhVien
{
    struct SinhVien
    {
        //field
        public String masv;
        public String hoTen;
        public double dtb;
        public DateTime ngaySinh;

        public SinhVien(string ma, string ten, double dtb, DateTime ns)
        {
            masv = ma;
            hoTen = ten;
            this.dtb = dtb;
            ngaySinh = ns;
        }
    }
    internal class QLSinhVien
    {
        static void NhapDS(SinhVien[] arr)
        {
            int ngay, thang, nam;

            for (int i = 0; i < arr.Length; i++)
            {
                // nhap sv arr[i]
                Console.WriteLine("Nhap masv:");
                arr[i].masv = Console.ReadLine();
                Console.WriteLine("Nhap ho ten");
                arr[i].hoTen = Console.ReadLine();
                Console.WriteLine("Nhap dtb: ");
                arr[i].dtb = double.Parse(Console.ReadLine());
                Console.WriteLine("Nhap ngay, thang, nam: ");
                ngay = int.Parse(Console.ReadLine());
                thang = int.Parse(Console.ReadLine());
                nam = int.Parse(Console.ReadLine());
                arr[i].ngaySinh = new DateTime(nam, thang, ngay);
            }
        }

        static void XuatDS(SinhVien[] arr)
        {
            Console.WriteLine($"{"MASV", 5} {"HO TEN", 15} {"DTB", 10} {"NGAY SINH", 15}");
            for (int i = 0; i < arr.Length; i++)
            {
                //XUAT THONG TIN SV arr[i]
                Console.WriteLine($"{arr[i].masv,5} {arr[i].hoTen,15} {arr[i].dtb,10} {arr[i].ngaySinh.ToString("dd/MM/yyyy"),15}");
            }
        }

        static int TimkiemTuanTu(SinhVien[] arr, string masv)
        {
            for (int i = 0; i < arr.Length; i++)
            {
                if (arr[i].masv == masv)
                    return i;
            }

            return -1;
        }

        static void Main(string[] args)
        {
            //luu tru duoc danh sach doi tong sinh vien
            int n;
            Console.WriteLine("Nhap so luong sv: ");
            n = int.Parse(Console.ReadLine());

            SinhVien[] arrSV = new SinhVien[n];

            NhapDS(arrSV);
            XuatDS(arrSV);

            string masv;
            System.Console.WriteLine("Nhap masv can tim: ");
            masv = Console.ReadLine();
            int viTri = TimkiemTuanTu(arrSV, masv);

            //1.Xem toan bo thong tin cua sv
            if (viTri != -1)
            {
                // xuat thong tin sv tim duoc arr[viTri]
                XuatSV(arrSV);
            }
            else Console.WriteLine("Khong ton tai sv");


            // 2. Ham Sua nam sinh cua sv do: 
            SuaThongTin(arrSV, viTri);

            //3. Ham xoa sv: 
            XoaPhanTu(arrSV, viTri);
            XuatDS(arrSV);

            /*
             * Viet ham Tim sv co ma sv la x bat ky. Sau khi tim thay hay viet ham
             * 1.Xem toan bo thong tin cua sv
             * +0.5
             * 2. Ham Sua nam sinh cua sv do: 
             * 3. Ham xoa sv: 
             */

        }

        static void XuatSV(SinhVien sv)
        {
            Console.WriteLine($"{"MASV",5} {"HO TEN",15} {"DTB",10} {"NGAY SINH",15}");
            Console.WriteLine($"{sv.masv,5} {sv.hoTen,15} {sv.dtb,10} {sv.ngaySinh.ToString("dd/MM/yyyy"),15}");
        }

        static void SuaThongTin(SinhVien[]arr, int viTri)
        {
            if (viTri >= 0 && viTri < arr.Length)
            {
                Console.WriteLine("Nhap nam sinh moi");
                int nam = int.Parse(Console.ReadLine());

                arr[viTri].ngaySinh = new DateTime(nam, arr[viTri].ngaySinh.Month, arr[viTri].ngaySinh.Day);
                Console.WriteLine("==> Thong tin sv sau khi duoc sua: ");
                XuatSV(arr[viTri]); // xem lai thong tin da luu chua
            }
        }

        static void XoaPhanTu(ref SinhVien[] arr, int viTri)
        {
            if (viTri >= 0 && viTri < arr.Length) // arr: 6 7 8 3 -, viTri = 2
            {
                for (int i = viTri + 1; i < arr.Length; i++) // i chi vao nhung vi tri can di doi
                {
                    arr[i - 1] = arr[i];
                }
                //thu hoi o nho du o cuoi mang
                Array.Resize(ref arr, arr.Length - 1);
            }
            else Console.WriteLine("Vi tri can xoa khong ton tai trong ds");
        }


    }
}
