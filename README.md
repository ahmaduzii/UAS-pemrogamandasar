# Sistem Manajemen Waktu Kerja Karyawan

from datetime import datetime

class WorkTimeManagement:
    def _init_(self):
        self.records = {}

    def clock_in(self, employee_id):
        now = datetime.now()
        if employee_id in self.records and "clock_in" in self.records[employee_id]:
            print(f"Karyawan {employee_id} sudah melakukan clock-in pada {self.records[employee_id]['clock_in']}.")
        else:
            self.records[employee_id] = {"clock_in": now}
            print(f"Karyawan {employee_id} berhasil clock-in pada {now}.")

    def clock_out(self, employee_id):
        now = datetime.now()
        if employee_id in self.records and "clock_in" in self.records[employee_id]:
            self.records[employee_id]["clock_out"] = now
            clock_in_time = self.records[employee_id]["clock_in"]
            total_hours = (now - clock_in_time).seconds / 3600
            self.records[employee_id]["total_hours"] = total_hours
            print(f"Karyawan {employee_id} berhasil clock-out pada {now}. Total jam kerja: {total_hours:.2f} jam.")
        else:
            print(f"Karyawan {employee_id} belum melakukan clock-in.")

    def view_records(self):
        if self.records:
            print("Rekaman Waktu Kerja:")
            for employee_id, times in self.records.items():
                print(f"Karyawan {employee_id}:")
                print(f"  Clock-in: {times.get('clock_in', 'Belum clock-in')}")
                print(f"  Clock-out: {times.get('clock_out', 'Belum clock-out')}")
                print(f"  Total Jam Kerja: {times.get('total_hours', 0):.2f} jam")
        else:
            print("Belum ada data rekaman.")

if _name_ == "_main_":
    wtm = WorkTimeManagement()
    while True:
        print("\nMenu:")
        print("1. Clock-in Karyawan")
        print("2. Clock-out Karyawan")
        print("3. Lihat Rekaman Waktu Kerja")
        print("4. Keluar")
        choice = input("Pilih menu (1-4): ")
  
        if choice == "1":
            emp_id = input("Masukkan ID Karyawan: ")
            wtm.clock_in(emp_id)
        elif choice == "2":
            emp_id = input("Masukkan ID Karyawan: ")
            wtm.clock_out(emp_id)
        elif choice == "3":
            wtm.view_records()
        elif choice == "4":
            print("Keluar dari program.")
            break
        else:
            print("Pilihan tidak valid. Coba lagi.")
