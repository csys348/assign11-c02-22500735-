Project Structure: 주요 파일 3개의 역할

    App.jsx : 전체 레이아웃 및 컴포넌트 호출
    CourseList.jsx : CRUD 및 목록 담당
    CourseItem.jsx : 목록 표시 담당

Component & Props: CourseList와 CourseItem의 관계 및 Props 전달 방식

    CourseList.jsx -> CourseItem.jsx의 부모 자식 관계
    부모는 데이터와 이벤트 헨들러를 내리고 자식은 UI를 그리고 사용자 조작에 대해 부모 호출

State & Event: useState를 이용한 상태 관리 및 삭제 버튼의 동작 원리

    CourseList에서 useState로 과목 배열 courses를, useState로 newName을 관리

    CourseItem의 Delete버튼을 클릭하면 onClick을 통해 onDelete가 실행되어 부모의 HendleDelete가 호출
    handleDelete는 삭제 여부 확인 후 취소를 누르면 즉시 반환
    확인을 누르면 기존 배열을 직접 수정하지 않고 해당 Id만 제외한 새 배열을 만들어 상태를 갱신
    상태가 바뀌면 CourseList가 리랜더링되면서 과목 목록과 상단 통계가 함께 업데이트

Code Analysis: 주요 코드 2개(각 5~15줄)를 선택하여 동작 원리 설명

      function handleDelete(id) {
    if (!window.confirm('이 과목을 삭제하시겠습니까?')) return;
    setCourses(previous => previous.filter(course => course.id !== id));

}

    previous=>previous.filter 형태의 함수형 업데이트를 통해 최신 상태를 기준으로 삭제 대상만 걸러낸 새 배열을 반환하여 불변성 유지

    <div className="course-main">
        <input
          className="check"
          type="checkbox"
          checked={course.completed}
          onChange={() => onToggle(course.id)}
          aria-label={`${course.name} 완료 여부`}
        />
        <div>
          <div className={`course-title ${course.completed ? "done" : ""}`}>
            {course.name}
          </div>
          <div className="course-id">Course #{course.id}</div>
        </div>
      </div>

      부모로부터 받은 course.complented를 checked에 바인드해 체크 상태를 동기화하고 Onchange로 부모의 ontoggle를 호출
