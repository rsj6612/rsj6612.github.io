---
title: "Dialogue Editor"
date: 2024-07-03 12:55:00 +09:00
categories: [Unity]
tags:
  [
    unity,
    RPG
  ]
---
# Dialogue Editor

rpg게임을 만들면서 npc와 대화하는 기능을 만드는데 코드로 구현하면서 만들어놓은 대화가 자꾸 배열에 저장이 안되거나 유니티를 껐다가 키면 사라지는 현상이 생겨 포기하고 다른 방법을 찾아보던 중 유튜브를 통해 Dialogue Editor라는 에셋을 알게 되었다. 

## Dialogue Editor
[에셋 스토어](https://assetstore.unity.com/packages/tools/utilities/dialogue-editor-168329)에서 다운받을 수 있다. Dialogue Editor는 Npc와 간단하게 대화를 할 수 있는 기능을 제공해준다.

## 과정

![1](/assets/images/postsImg/1.png')
우선 캔버스가 있기 때문에 메인 캔버스 아래로 ConversationManager 오브젝트를 넣었다.  화면 가운데에 대화창이 생긴 것을 볼 수 있다. 저곳에 이제 만드는 대화들이 들어간다. 적절한 위치에 둔다.

![2](/assets/images/postsImg/2.png')
![3](/assets/images/postsImg/3.png')
빈 게임오브젝트를 만들어 이곳에 NPCConversation 스크립트를 넣는다. 다운받은 에셋에 있다.

![4](/assets/images/postsImg/4.png')
그리고 Window -> Dialgue Editor 탭을 열면 이러한 화면이 나온다. 처음에 오른쪽에 있는 설정들은. 디폴트 설정값으로 설정해두면 만들 때 디폴트로 설정값들이 들어간다.

![5](/assets/images/postsImg/5.png')
이제 가운 창을 클릭하면 설정할 것들이 달라지는데,

![6](/assets/images/postsImg/6.png')
이런 식으로 NPC의 이름, 대화 내용, 왼쪽에 아이콘, 음성, 폰트 등을 설정할 수가 있다. 근데 NPC의 이름은 한글이 안되는 듯하다.

![7](/assets/images/postsImg/7.png')
나는 이런 식으로 설정하였다. 초록색으로 이어진 것은 가운데 창을 우클릭하면 Create Option이라는 것이 있는데, 대화의 선택지를 만드는 것이다.

그리고 NPC 오브젝트에 새로운 스크립트를 작성해주면 된다.

[참고 유튜브](https://www.youtube.com/watch?v=QPJHY6MPag4&t=255s)
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using DialogueEditor;

public class ConversationStarter : MonoBehaviour {
[SerializeField] private NPCConversation myConversation;

private void OnTriggerStay(Collider Other) {
    if (Other.CompareTag("Player") {
       if (Input.GetKeyDown(KeyCode.F) {
          ConversationManager.Instance.StartConversation(myConversation)
         }
      }
   }
}
```
이 코드는 유튜브에 있는 것을 그대로 따온 것으로 플레이어 태그를 찾고 F키를 누르면 대화창이 활성화되게 하는 것이다. 나는 G키를 누르라는 안내 문구, 그리고 유니티의 new input system을 사용해서 코드를 참고만 하고 변형해서 사용하였다. 트리거 또한 NPC에 따로 만들어 isTrigger를 활성화 시켜야 한다.


## 결과
![8](/assets/images/postsImg/8.png')
![9](/assets/images/postsImg/9.png')
트리거에 닿으면 G키를 누르라는 안내 문구와 함께 누르면 내가 아까 설정하고 만들었던 선택지를 가진 대화창이 나온 것을 볼 수 있다.



 