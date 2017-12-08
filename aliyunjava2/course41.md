## [上一页](course40)

##  【第03个代码模型】综合案例：数据表与简单JAVA类（多对多）

定义一个学生选课的操作表：三张数据表

- 学生表：学生编号、姓名、年龄

- 课程表：课程编号、课程名称、学分

- 学生-课程关系表：学生编号、课程编号、成绩

要求可以实现如下的信息输出：

- 找到一门课程以及参加此课程的所有学生信息和他的成绩

- 根据一个学生，找到所有参加的课程和成绩

1、 定义出基本类，暂时不考虑所有的关系。

	class Student {
		private int stuid;
		private String name;
		private int age;
		public Student() {}
		public Student(int stuid, String name, int age) {
			this.stuid = stuid;
			this.name = name;
			this.age = age;
		}
		public String getInfo() {
			return "【STUDENT】 学生编号： " + this.stuid + ", 姓名： " + this.name +
					", 年龄： " + this.age ;
		}
	}
	
	class Course {
		private int cid;
		private String name;
		private int credit;
		public Course() {}
		public Course(int cid , String name, int credit) {
			this.cid = cid;
			this.name = name;
			this.credit = credit;
		}
		public String getInfo() {
			return "【COURSE】 课程编号： " + this.cid + ", 名称 "+ this.name 
					+ ", 学分： " + this.credit;
		}
	}

2 、 一个学生有多门课，一门课有多个学生选择，所以应该保存有各自的对象数组。

	class Student {
		private int stuid;
		private String name;
		private int age;
		private Course[] courses;
		
		public Student() {}
		public Student(int stuid, String name, int age) {
			this.stuid = stuid;
			this.name = name;
			this.age = age;
		}
		
		public void setCourses(Course[] courses) {
			this.courses = courses;
		}
		public Course[] getCourses() {
			return this.courses;
		}
		
		public String getInfo() {
			return "【STUDENT】 学生编号： " + this.stuid + ", 姓名： " + this.name +
					", 年龄： " + this.age ;
		}
	}
	
	class Course {
		private int cid;
		private String name;
		private int credit;
		private Student[] students;
		
		public Course() {}
		public Course(int cid , String name, int credit) {
			this.cid = cid;
			this.name = name;
			this.credit = credit;
		}
		
		public void setStudents(Student[] students) {
			this.students = students;
		}
		public Student[] getStudents() {
			return this.students;
		}
		
		public String getInfo() {
			return "【COURSE】 课程编号： " + this.cid + ", 名称 "+ this.name 
					+ ", 学分： " + this.credit;
		}
	}

3、 学生和每门课之间都会有一个成绩。关系表中不光有关系字段还有普通字段，应该再建立一个类。

	class StudentCourse{
		private Student student;
		private Course course;
		private double score;
			
		public StudentCourse() {}
		public StudentCourse(Student student, Course course , double score) {
			this.student = student;
			this.course = course;
			this.score = score;
		}
			
		public Student getStudent() {
			return this.student;
		}
		public Course getCourse() {
			return this.course;
		}
		public double getScore() {
			return this.score;
		}
	}

学生和课程通过StudentCourse类来对应：

	class Student {
		private int stuid;
		private String name;
		private int age;
		private StudentCourse[] studentCourses;
		
		public Student() {}
		public Student(int stuid, String name, int age) {
			this.stuid = stuid;
			this.name = name;
			this.age = age;
		}
		
		public void setStudentCourse(StudentCourse[] studentCourses) {
			this.studentCourses = studentCourses;
		}
		public StudentCourse[] getStudentCourse() {
			return this.studentCourses;
		}
		
		public String getInfo() {
			return "【STUDENT】 学生编号： " + this.stuid + ", 姓名： " + this.name +
					", 年龄： " + this.age ;
		}
	}
	
	class Course {
		private int cid;
		private String name;
		private int credit;
		private StudentCourse[] studentCourses;
		
		public Course() {}
		public Course(int cid , String name, int credit) {
			this.cid = cid;
			this.name = name;
			this.credit = credit;
		}
		
		public void setStudentCourse(StudentCourse[] studentCourses) {
			this.studentCourses = studentCourses;
		}
		public StudentCourse[] getStudentCourse() {
			return this.studentCourses;
		}
		
		public String getInfo() {
			return "【COURSE】 课程编号： " + this.cid + ", 名称 "+ this.name 
					+ ", 学分： " + this.credit;
		}
	}

4、 要进行操作的实现

	class Student {
		private int stuid;
		private String name;
		private int age;
		private StudentCourse[] studentCourses;
		
		public Student() {}
		public Student(int stuid, String name, int age) {
			this.stuid = stuid;
			this.name = name;
			this.age = age;
		}
		
		public void setStudentCourse(StudentCourse[] studentCourses) {
			this.studentCourses = studentCourses;
		}
		public StudentCourse[] getStudentCourse() {
			return this.studentCourses;
		}
		
		public String getInfo() {
			return "【STUDENT】 学生编号： " + this.stuid + ", 姓名： " + this.name +
					", 年龄： " + this.age ;
		}
	}
	
	class Course {
		private int cid;
		private String name;
		private int credit;
		private StudentCourse[] studentCourses;
		
		public Course() {}
		public Course(int cid , String name, int credit) {
			this.cid = cid;
			this.name = name;
			this.credit = credit;
		}
		
		public void setStudentCourse(StudentCourse[] studentCourses) {
			this.studentCourses = studentCourses;
		}
		public StudentCourse[] getStudentCourse() {
			return this.studentCourses;
		}
		
		public String getInfo() {
			return "【COURSE】 课程编号： " + this.cid + ", 名称 "+ this.name 
					+ ", 学分： " + this.credit;
		}
	}
	
	class StudentCourse{
		private Student student;
		private Course course;
		private double score;
		
		public StudentCourse() {}
		public StudentCourse(Student student, Course course , double score) {
			this.student = student;
			this.course = course;
			this.score = score;
		}
		
		public Student getStudent() {
			return this.student;
		}
		public Course getCourse() {
			return this.course;
		}
		public double getScore() {
			return this.score;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			//第一步： 根据结构进行关系的设置
			//1、创建各自的独立对象
			Student stu1 = new Student(1, "张三", 18);
			Student stu2 = new Student(2, "李四", 19);
			Student stu3 = new Student(3, "王五", 18);
			Course ca = new Course(1001, "马克思主义哲学", 3);
			Course cb = new Course(1002, "操作系统", 2);
			//2、 需要设置学生和课程的关系，这里面需要准备出成绩
			stu1.setStudentCourse(new StudentCourse[] {
					new StudentCourse(stu1, ca, 99.9), 
					new StudentCourse(stu1, cb, 87.0)
				});
			stu2.setStudentCourse(new StudentCourse[] {
					new StudentCourse(stu2, ca, 78.9)
				});
			stu3.setStudentCourse(new StudentCourse[] {
					new StudentCourse(stu3, cb, 98.9)
				});
			//3、 设置课程和学生关系
			ca.setStudentCourse(new StudentCourse[] {
					new	StudentCourse(stu1, ca, 99.9),
					new StudentCourse(stu2, ca, 78.9)
				});
			cb.setStudentCourse(new StudentCourse[] {
					new	StudentCourse(stu1, cb, 87.0),
					new StudentCourse(stu3, cb, 98.9)
				});
			//第二步：根据结构取出数据
			//1、  找到一门课程以及参加此课程的所有学生信息和他的成绩
			System.out.println(ca.getInfo());
			for(int x = 0 ; x < ca.getStudentCourse().length;x++) {
				System.out.print("\t|- " + ca.getStudentCourse()[x].getStudent().getInfo());
				System.out.print(", 成绩 " + ca.getStudentCourse()[x].getScore());
				System.out.println();
			}
			System.out.println("====================================");
			System.out.println(stu1.getInfo());
			for(int x = 0;x < stu1.getStudentCourse().length ; x ++) {
				System.out.print("\t|- " + stu1.getStudentCourse()[x].getCourse().getInfo());
				System.out.print("，成绩 " + stu1.getStudentCourse()[x].getScore());
				System.out.println();
			}
		}
	}

**course：**

	【COURSE】 课程编号： 1001, 名称 马克思主义哲学, 学分： 3
		|- 【STUDENT】 学生编号： 1, 姓名： 张三, 年龄： 18, 成绩 99.9
		|- 【STUDENT】 学生编号： 2, 姓名： 李四, 年龄： 19, 成绩 78.9
	====================================
	【STUDENT】 学生编号： 1, 姓名： 张三, 年龄： 18
		|- 【COURSE】 课程编号： 1001, 名称 马克思主义哲学, 学分： 3，成绩 99.9
		|- 【COURSE】 课程编号： 1002, 名称 操作系统, 学分： 2，成绩 87.0

这些关系的开发模式必须灵活编写。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course42)
