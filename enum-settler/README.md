# Enum 활용기

안녕하세요? 우아한 형제들에서 결제/정산 시스템을 개발하고 있는 이동욱입니다.  
  
상반기 저희팀 최대 과제인 정산 플랫폼 개편을 진행함에 있어 저에게 큰 힘이 되었던 Enum를 어떻게 사용했는지에 대해 정리하게 되었습니다.  
  
Java의 기본서에 빠지지 않고 등장했지만, 그간 필요성을 못느끼고 있던 때에 좋은 기회가 생겨 많이 활용할 수 있었습니다.  
  
어마어마한 비법이나 신기술을 담은 내용은 없지만, 보시는 분들에게 조금이나마 도움이 되었으면 하는 바램입니다.

> 나 : 선임님 코드 "card"는 뭔가요?  

> 선임님 : PG 결제에요

...
> 나 : 선임님 여기서 "card"도 PG죠?

> 선임님 : 아 여기선 카드에요

...?


## 들어가며

여기서 사용된 코드는 실제 회사에서 사용한 코드는 아니며, 포스팅을 위해 별도 샘플로 작성한 코드임을 먼저 말씀드립니다.  
  
이해를 돕기 위해 몇가지 유형을 구분지었습니다.  
어떤 상황에서 Enum을 통해 어떻게 해결 되었는지에 대해 작성하였습니다.  

## 유형

### 데이터 전환

여러 시스템과 연계되다보니 **동일한 데이터를 서로 다른 API 스펙에 맞춰** 전달받고 / 전달해야하는 경우가 있습니다.  
  
예를 들어 A API에서는 상태값을 "Y", "N" 으로 전달주는데, 이를 B API에 "1", "0"으로 전달하고, C API에는 true, false로 전달하는 기능입니다.  

if문으로 전부 처리되다보니 몇가지 문제가 있었습니다.

* 일단 코드가 너무 지저분합니다.
* 상태값이  



### 중복된 코드명

결제라는 데이터는 결제의 종류와 결제 수단이라는 2가지 형태로 표현됩니다.  
예를 들어 신용카드 결제는 **신용카드 결제**가 결제 수단이며, **카드 결제**라는 결제 종류에 포함됩니다.  
이 카드 결제 종류에는 페이코, 카카오 페이등 여러 결제 수단이 포함되어 있다고 생각하시면 될것 같습니다.  


### 무분별한 DB 사용


### Layer별 분리된 관리 포인트

정산 플랫폼은 수많은 카테고리가 존재하기 때문에 UI에서 select box로 표현되는 부분이 많습니다.  



## 마무리

A라는 상황에서 "a"와 B라는 상황에서 "a"는 전혀 다른 의미입니다.  
문자열은 이런 상황까지 담을 수 없습니다.
하지만 Enum은 **문맥(Context)을 담을 수 있습니다**.
if문 1~2줄로 해결할 수도 있으며,
테이블을 생성해서 row로 해결할 수 도 있었습니다.

그럼에도 이렇게 Enum을 
더군다나 이 코드의 의미와 용도를 파악하기 위해 컨플루언스를 찾고, 엑셀과 워드 파일을 뒤지고, 레거시 테이블을 Join & Group by 하고, PHP 코드를 다시 찾는 과정이 정말 정말 **비효율적**이라고 생각하였습니다.  


문서는 일반적으로 해당 시스템을 잘 아시는 분이 작성하게 됩니다.  
역설적이게도 그렇기 때문에 그 분의 입장에서 **당연한 내용이 누락**되는 경우가 빈번합니다.  

데이터베이스는 결국 행위를 담지는 못합니다.  