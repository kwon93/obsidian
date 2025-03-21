- backend UI 요구사항
	- 
- frontend UI 요구사항  
	- 대만 Image 추가로 이미지 출력란 증가 
		-  한 화면에 모두 들어오기 애매할 경우 스크롤 추가 고려 혹은 테이블 형태의 UI 외에 다른 방안 고려
	- 가동브라켓 추가로 단축키를 활용한 멀티 커서 지원 
		- Number Pad를 활용해 1 + Click 형식으로 여러개의 Boxing을 가능하게해야함. 
		- 하나의 이미지에 가동브라켓이 여러개일 경우 테이블에도 추가 가동브라켓만큼의 record가 추가되야함 
			- 기존 record 에서 다중 가동브라켓일경우 클릭시 dropDown되어 숨어있던 그 외 가동브라켓값이 보여지도록 
			- 단축키를 활용해서 A와 D를 활용해 드랍다운메뉴를 펼치고 접을 수 있도록 ( 펼쳐진 드랍다운 메뉴에서도 값 수정 및 업데이트가 가능해야함. )
	 - 전주 구간별 m 별로 동적 통계를 낸 셀렉트 박스 추가 
		 - 이상 전주 구간만 빠르게 파악하여 수동 검수 할 수 있도록
	 - 사용되고있지않은 값들은 테이블에서 제거 
		 - poleH , poleW 등 현재 사용되고있지않는 컬럼은 삭제 

---
화면에 출력할 중간 테이블

공통 테이블
pole_index | track | track_unit | date | pole_x (대표값) | pole_y(대표값) | PDS-OCR/L | PDS-OCR/R | TSI-OCR/L | TSI-OCR/R | overlap (*가동브라켓 갯수)

보조 테이블
count | pole_index | pole_x | pole_y

---
중간 테이블 확정 column 

id  
track  
track_unit  
date  
image_index  
pole_number  
pole_index  
pole_x 
pole_y  *다중 가동브라켓 ??*
pds_lon  
pds_lat  
tsi_lon  
tsi_lat  
pixel_count  
tacho  
PDS-OCR/L  
PDS-OCR/R  
TSI-OCR/L  
TSI-OCR/R  
LSI_name  * name은 이미지 파일 이름*
PDS_name  
TSI_name  
overlap
distance