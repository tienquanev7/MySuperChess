public class Student {
    private String name;
    private String id;
    private String group;
    private String email;

    public Student() {
        this.name = "Student";
        this.id = "000";
        this.group = "K62CB";
        this.email = "uet@vnu.edu.vn";
    }

    public Student(String name, String id, String email) {
        this.name = name;
        this.id = id;
        this.email = email;
        this.group = "K62CB";
    }

    public Student(Student s) {
        this.name = s.name;
        this.id = s.id;
        this.group = s.group;
        this.email = s.email;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getId() {
        return id;
    }

    public String getEmail() {
        return email;
    }

    public String getInfo() {
        return name + " - " + id + " - " + group + " - " + email;
    }
}
java
Copy code
public class StudentManagement {
    private Student[] students;
    private int studentCount;

    public StudentManagement() {
        this.students = new Student[100];
        this.studentCount = 0;
    }

    public void addStudent(Student newStudent) {
        if (studentCount < 100) {
            students[studentCount] = newStudent;
            studentCount++;
        }
    }

    public static boolean sameGroup(Student s1, Student s2) {
        return s1.group.equals(s2.group);
    }

    public String studentsByGroup() {
        StringBuilder result = new StringBuilder();

        // Lấy danh sách các lớp
        String[] groups = new String[studentCount];
        int groupCount = 0;
        for (int i = 0; i < studentCount; i++) {
            boolean isNewGroup = true;
            for (int j = 0; j < groupCount; j++) {
                if (students[i].group.equals(groups[j])) {
                    isNewGroup = false;
                    break;
                }
            }
            if (isNewGroup) {
                groups[groupCount] = students[i].group;
                groupCount++;
            }
        }

        // Sắp xếp các lớp
        for (int i = 0; i < groupCount; i++) {
            result.append(groups[i]).append("\n");
            for (int j = 0; j < studentCount; j++) {
                if (students[j].group.equals(groups[i])) {
                    result.append(students[j].getInfo()).append("\n");
                }
            }
        }

        return result.toString();
    }

    public void removeStudent(String id) {
        for (int i = 0; i < studentCount; i++) {
            if (students[i].getId().equals(id)) {
                // Di chuyển các sinh viên phía sau lên trước để thay thế sinh viên cần xóa
                for (int j = i; j < studentCount - 1; j++) {
                    students[j] = students[j + 1];
                }
                studentCount--;
                break;
            }
        }
    }

    public static void main(String[] args) {
        StudentManagement management = new StudentManagement();

        Student student1 = new Student("Nguyen Van An", "17020001", "17020001@vnu.edu.vn");
        Student student2 = new Student("Nguyen Van B", "17020002", "17020002@vnu.edu.vn");
        Student student3 = new Student("Nguyen Van C", "17020003", "17020003@vnu.edu.vn");
        Student student4 = new Student("Nguyen Van D", "17020004", "17020004@vnu.edu.vn");

        management.addStudent(student1);
        management.addStudent(student2);
        management.addStudent(student3);
        management.addStudent(student4);

        System.out.println("Danh sách sinh viên theo lớp:\n" + management.studentsByGroup());

        management.removeStudent("17020002");

        System.out.println("Danh sách sinh viên sau khi xóa:\n" + management.studentsByGroup());
    }
}
Lớp StudentManagement có các phương thức để thêm, kiểm tra cùng lớp, in danh sách theo lớp, và xóa sinh viên theo mã số. Chú ý rằng danh sách sinh viên được lưu trong mảng và có giới hạn tối đa là 100 sinh viên.





Send a message
