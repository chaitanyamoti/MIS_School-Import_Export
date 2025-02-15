🏫 School Management Information System (MIS)
A Django-based School MIS for managing student records, attendance, exams, subject assignments, and dynamic filtering for exporting students.

🚀 Features
✔ Student Management (Enroll, update, delete)
✔ Class & Subject Management (Assign subjects to classes)
✔ Teacher Management
✔ Attendance Tracking
✔ Exam & Marks Management
✔ Dynamic Student Filtering in Admin
✔ Export Only Filtered Students (e.g., Hostel students)

📂 Project Structure
csharp
Copy
Edit
school_mis/
│── core/                     # Main app (students, teachers, subjects)
│── exams/                    # Exam-related models & views
│── school_mis/               # Project settings & URLs
│── templates/                # HTML templates (if applicable)
│── static/                   # CSS, JS, images (if applicable)
│── manage.py                 # Django management script
│── requirements.txt          # Required Python packages
│── README.md                 # Documentation
🔧 Installation & Setup
1️⃣ Clone the Repository
sh
Copy
Edit
git clone https://github.com/your-repo/school-mis.git
cd school-mis
2️⃣ Create a Virtual Environment
sh
Copy
Edit
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
3️⃣ Install Dependencies
sh
Copy
Edit
pip install -r requirements.txt
4️⃣ Apply Migrations
sh
Copy
Edit
python manage.py makemigrations
python manage.py migrate
5️⃣ Create a Superuser (Admin)
sh
Copy
Edit
python manage.py createsuperuser
👉 Enter username, email, password when prompted.

🛠 Running the Project
sh
Copy
Edit
python manage.py runserver
🔗 Open http://127.0.0.1:8000/admin/ in your browser.

Login with the superuser credentials to manage data.

📊 Dynamic Student Filtering & Export
✔ Filter by hostel students, class, or other fields in Django Admin
✔ Export only the currently filtered students

🔹 How to Use:

Go to Admin → Students
Apply filters (e.g., select only hostel students)
Click Export → The exported file contains only the filtered students
📝 Admin Setup (Django Admin)
Modify admin.py to add filtering & export functionality:

python
Copy
Edit
from django.contrib import admin
from import_export import resources
from import_export.admin import ExportMixin
from .models import Student

class StudentResource(resources.ModelResource):
    class Meta:
        model = Student

    def export_queryset(self, queryset):
        return queryset  # Export only currently filtered data

class StudentAdmin(ExportMixin, admin.ModelAdmin):
    resource_class = StudentResource
    list_filter = ['is_hostel_student', 'school_class']
    list_display = ['name', 'school_class', 'is_hostel_student']

    def get_export_queryset(self, request):
        queryset = super().get_queryset(request)
        filter_params = request.GET.dict()  # Capture applied filters
        return queryset.filter(**filter_params)  # Apply selected filters

admin.site.register(Student, StudentAdmin)
📌 Technologies Used
🔹 Django (Backend)
🔹 SQLite / PostgreSQL (Database)
🔹 Django Import-Export (Data import/export)
🔹 Bootstrap / CSS (Frontend UI)

📢 Contributing
✅ Fork the repo
✅ Create a feature branch (git checkout -b feature-name)
✅ Commit your changes (git commit -m "Added new feature")
✅ Push to the branch (git push origin feature-name)
✅ Open a Pull Request

💡 Future Improvements
✅ Advanced filtering (by date, performance, attendance, etc.)
✅ Improved UI for admin dashboard
✅ Student report generation