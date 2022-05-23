## :star_of_david: DAO 없이 DTO 와 Java main 함수를 통한 DB 조작 코드

### :rocket:**DAO 의 역할 ( CRUD 1탄)**



- `DTO(Data Transfer Object)` 는 계층 간 데이터 교환을 하기 위해 사용하는 객체로, DTO는 로직을 가지지 않는 순수한 데이터 객체(getter & setter 만 가진 클래스)입니다.

- `DAO(Data Access Object)` 는 데이터베이스의 data에 접근하기 위한 객체입니다. **DataBase에 접근 하기 위한 로직 & 비지니스 로직**을 분리하기 위해 사용합니다.

  

DAO 를 사용하지않고 DTO**(Data Transfer Object)** 와 main 함수의 DB 접근으로 CRUD 를 간단하게 동작해보겠다.

현재는 DB 를 연동하지 않은상태로 HashMap() 을이용하여 하드코딩하여 일단  DB  역할로 사용하였다.

`DTO 코드`

```java
package manager;

import java.util.Date;

public class MemberDTO {
	private int num;
	private String memberId;
	private String memberPw;
	private String nickName;
	private Date regdate; // java.util.Date

	public MemberDTO(int num, String memberId, String memberPw, String nickName) {
		super();
		this.num = num;
		this.memberId = memberId;
		this.memberPw = memberPw;
		this.nickName = nickName;
	}

	public int getNum() {
		return num;
	}

	public void setNum(int num) {
		this.num = num;
	}

	public String getMemberId() {
		return memberId;
	}

	public void setMemberId(String memberId) {
		this.memberId = memberId;
	}

	public String getMemberPw() {
		return memberPw;
	}

	public void setMemberPw(String memberPw) {
		this.memberPw = memberPw;
	}

	public String getNickName() {
		return nickName;
	}

	public void setNickName(String nickName) {
		this.nickName = nickName;
	}

	public Date getRegdate() {
		return regdate;
	}

	public void setRegdate(Date regdate) {
		this.regdate = regdate;
	}

	@Override
	public String toString() {
		return "MemberVo [num=" + num + ", memberId=" + memberId + ", memberPw=" + memberPw + ", nickName=" + nickName
				+ ", regdate=" + regdate + "]";
	}

}

```

`main`

```java
package manager;

import java.util.ArrayList;
import java.util.Date;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.*;
public class Main {

	public static void main(String[] args) {
		Map<Integer, MemberDTO> db = new HashMap<>();
		
		//C (insert)
		MemberDTO vo1 = new MemberDTO(1,"test1","1234","nick1");
		vo1.setRegdate(new Date());
		MemberDTO vo2 = new MemberDTO(2,"test2","1234","nick2");
		vo2.setRegdate(new Date());
		MemberDTO vo3 = new MemberDTO(3,"test3","1234","nick2");
		vo3.setRegdate(new Date());
		
		db.put(1,vo1);
		db.put(2,vo2);
		db.put(3,vo3);
		System.out.println("저장 완료!");
		
		//R (select)
		List<MemberDTO> ls = new ArrayList<>(db.values()); //컬렉션을 반환
		for(MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회완료");
		
		MemberDTO vo = null;
		vo = db.get(1);
		System.out.println(vo);
		
		vo = db.get(4);
		System.out.println(vo);
		System.out.println("조회 완료");
		//U (update)
		vo = db.get(1);
		System.out.println(vo);
		
		if( vo != null) {
			vo.setMemberPw("4321");
			vo.setNickName("1nick");
			db.put(vo.getNum(),vo);
		}
		vo = db.get(1);
		System.out.println(vo);
		System.out.println("수정");
		
		//D (delete)
		db.remove(2);
		ls = new ArrayList<>(db.values());
		for( MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회 완료");
		
		//전체삭제
		db.clear();
		System.out.println("전체삭제 완료");
	}

}

```

***

위 코드는 main 함수에서 db에 접근하고있는데 , DAO 를 만들어서 사용한다면

DAO **(Database Access Object)**  를사용하여 db 에 접근하고 main함수에서는 DAO 를 조작하는 코드로 리팩토링 해보겠다.

DAO 를 사용하는 가장큰 목적증 간단히 말하자면 비지니스적 로직을 분리하는데 목적이 있다.



`DAO 코드 `

```java
package manager;

import java.util.*;

public class MemberDAO {
	//db 역할
	private Map<Integer,MemberDTO> db = new HashMap<>();
	
	
	//C
	public void insertMember(MemberDTO DTO) {
		DTO.setRegdate(new Date());
		db.put(vo.getNum(),DTO);
	}
	//R
	public MemberDTO selectMember(int num) {
		return db.get(num);
	}
	
	public List<MemberDTO> selectMemberAll(){
		return new ArrayList<MemberDTO>(db.values());
	}
	
	//U
	public void updateMember(MemberDTO DTO) {
		db.put(DTO.getNum(),DTO);
		System.out.println("DAO "+vo.getNum()+" 번에 " +DTO +" 객체로 업데이트 완료");
	}
	
	//D
	public void deleteMember( int num ) {
		db.remove(num);
		System.out.println("DAO 에서 "+num +"번자료를 삭제했습니다.");
		
	}
	public void deleteMemberAll() {
		db.clear();
		System.out.println("DAO 에서 모든데이터를 삭제완료");
	}
	
}

```

`main2 코드`

```java
package manager;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class Main2 {

	public static void main(String[] args) {
		MemberDAO memberDAO = new MemberDAO();

		// C (insert)
		MemberDTO DTO1 = new MemberDTO(1, "test1", "1234", "nick1");
		DTO1.setRegdate(new Date());
		MemberDTO DTO2 = new MemberDTO(2, "test2", "1234", "nick2");
		DTO2.setRegdate(new Date());
		MemberDTO DTO3 = new MemberDTO(3, "test3", "1234", "nick2");
		DTO3.setRegdate(new Date());

		memberDAO.insertMember(DTO1);
		memberDAO.insertMember(DTO2);
		memberDAO.insertMember(DTO3);
		System.out.println("저장 완료!");

		// R (select)
		List<MemberDTO> ls = memberDAO.selectMemberAll();
		for (MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회완료");

		MemberDTO vo = null;
		DTO = memberDAO.selectMember(1);
		System.out.println(DTO);


		// U (update)
		DTO = memberDAO.selectMember(1);

		if (DTO != null) {
			DTO.setMemberPw("4321");
			DTO.setNickName("1nick");
			memberDAO.updateMember(DTO);
		}
		DTO = memberDAO.selectMember(1);

		// D (delete)
		memberDAO.deleteMember(2);
		ls = memberDAO.selectMemberAll();
		for (MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회 완료");

		// 전체삭제
		memberDAO.deleteMemberAll();
	}

}

```



main 을 카피하여 main2 를 만들어서 코드에 DAO 를 적용시켜 같은 동작을 하게 만들어보았다.

지금은 깊이있게 DAO 클래스를 조작해야하는 이유중 단면의 목적으로 사용하지만

위에 코드는 DAO 가 정말 DB 와 쿼리를 주고받는 정도로 이용했지만

JSP 와 서버를 동작시키며 소통시킬때는 처리하는 개념(연산,비교 등 비지니스로직,핵심기능) 이 필요할거다.

좀더 프로젝트를 진행해보고 넓은 의미로 왜 DAO 클래스를  분리시켜 관리하는 것이 어떤 이점들이 더있는지에 대한 공부를 계속 이어가려한다. 

***

### :rocket:**DAO 와 Service 역할 ( CRUD 2탄)**

* `MemberDAO 클래스`  는 database 와의 소통을 위한 목적이 크다.
  * DB 쪽 내용이 달라진다면 DAO 만 건들면되는것이고,

* `MemberService 클래스 ` 는 클라이언트의 요청이 무엇이냐에 따라서 요청에 관련된 처리하는곳 이라고 나눠생각을해보자.
  * Service 처리과정이 달라진다면 MemberSerive 를 건들면 된다.



​	:star: 객체지향의 관점에서 결합도를 낮춰주는다는 것, 역할들을 나눠서 관리한다.

DAO 클래스에서는 오로지 DB 와의 접근하는 로직만 작성하고, Service 에서는 조건,연산,처리 등의 기능적인부분을

담당하게 역할을 구분하는것이 좋다.



`MemberService 코드`

```java
package manager;

import java.util.List;

public class MemberService {
	private MemberDAO memberDAO;

	public MemberService(MemberDAO memberDAO) {
		this.memberDAO = memberDAO;
	}
	
	//등록하기
	
	public boolean regist(MemberDTO DTO) {
		if(memberDAO.selectMember(DTO.getNum()) == null) {
			memberDAO.insertMember(DTO);
			return true;
		}else {
			return false;
		}
	}
	
	//조회하기
	
	public MemberDTO read(int num) {
		return memberDAO.selectMember(num);
	}
	
	//전체조회기능
	public List<MemberDTO> listAll(){
		return memberDAO.selectMemberAll();
	}
	
	//수정
	public void edit(MemberDTO DTO) {
		MemberDTO searchMember = memberDAO.selectMember(DTO.getNum());
		
		if(searchMember.getMemberPw().equals(DTO.getMemberPw())) {
			memberDAO.updateMember(DTO);
		}
	}
	
	//탈퇴
	public void remove(int num) {
		memberDAO.deleteMember(num);
	}
}

```

`main3 코드`

```java
package manager;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class Main3 {

	public static void main(String[] args) {
		MemberService memberService = new MemberService(new MemberDAO());

		// C (insert)
		MemberDTO DTO1 = new MemberDTO(1, "test1", "1234", "nick1");
		DTO1.setRegdate(new Date());
		MemberDTO DTO2 = new MemberDTO(2, "test2", "1234", "nick2");
		DTO2.setRegdate(new Date());
		MemberDTO DTO3 = new MemberDTO(3, "test3", "1234", "nick2");
		DTO3.setRegdate(new Date());

		memberService.regist(DTO1);
		memberService.regist(DTO2);
		memberService.regist(DTO3);
		System.out.println("저장 완료!");

		// R (select)
		List<MemberDTO> ls = memberService.listAll();
		for (MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회완료");

		MemberDTO DTO = null;
		DTO = memberService.read(1);
		System.out.println(DTO);

		// U (update)
		DTO = memberService.read(1);

		if (DTO != null) {
			DTO.setMemberPw("4321");
			DTO.setNickName("1nick");
			memberService.edit(DTO);
		}
		DTO = memberService.read(1);

		// D (delete)
		memberService.remove(2);
		ls = memberService.listAll();
		for (MemberDTO tmp : ls) {
			System.out.println(tmp);
		}
		System.out.println("전체 조회 완료");
	}

}

```



DAO 와 Servic 클래스의 목적을 구분하여 DAO 는 DB 와의 접근 로직만으로 구분하고 Service 클래스에서는 DAO를 이용하며 서비스처리를위한 비지니스 로직으로 구분하여 사용하였는데 , 좀더 각자 목적에 맞게  역할을 구분하여 비지니스로직이 문제가있다면 Service 클래스를 살펴보면될것이고 , DB 접근 문제가 발생되었을때는 DAO 클래스만 살펴보면되기에 유지보수면에서도 안정적이게 되었다.

***



## :rocket:**DAO + Service + DB연동  ( CRUD 3탄)**
