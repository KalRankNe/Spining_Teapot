# Spining_Teapot
------------------------------------------
###  소감문

> 프로그래밍의 세계는 때때로 우리의 인내심을 시험하는 문제들로 가득 차 있습니다. C++을 활용한 주전자 회전 프로젝트는 그러한 도전의 일환으로, 라이브러리 다운로드와 설정 과정에서 예상치 못한 어려움에 직면했습니다. 그럼에도 불구하고, 이러한 장애물을 극복하는 과정에서 얻은 지식과 경험은 매우 가치 있는 것이었습니다.

------------------------------------------
#### Cpp소스코드
```cpp
#include <GL/glut.h>

// 회전 각도
float angle = 0.0f;

void init() {
    glClearColor(0.0, 0.0, 0.0, 1.0);
    glEnable(GL_DEPTH_TEST);
}

void display() {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glLoadIdentity();

    // 카메라 설정
    gluLookAt(0.0, 5.0, 5.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0);

    glRotatef(angle, 0.0f, 1.0f, 0.0f); // Y 축 주위로 회전

    // 주전자 모델 렌더링
    glutWireTeapot(1.0);

    glutSwapBuffers();
}

void reshape(int w, int h) {
    glViewport(0, 0, w, h);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(45.0, (double)w / (double)h, 1.0, 200.0);
    glMatrixMode(GL_MODELVIEW);
    glLoadIdentity();
}

void timer(int value) {
    angle += 2.0f; // 회전 속도
    glutPostRedisplay();
    glutTimerFunc(16, timer, 0); // 60fps
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
    glutInitWindowSize(800, 600);
    glutCreateWindow("Teapot Rotation");

    init();

    glutDisplayFunc(display);
    glutReshapeFunc(reshape);
    glutTimerFunc(0, timer, 0);

    glutMainLoop();
    return 0;
}
```
