# Mecab-Install
If the installing mecab failed, try this


https://provia.tistory.com/57



최근 Kakao에서 Khaiii를 발표해서 조금 인기가 약해지긴 했지만, 여전히 Khaiii와 맞먹는 성능을 보여주는 mecab설치를 진행해 보도록 하겠습니다.

 

1. 우선 mecab 홈페이지에서 최신 버전을 다운로드 합니다. 

    현재는 mecab-0.996-ko-0.9.2.tar.gz 이 파일이 최신이네요.

 

https://bitbucket.org/eunjeon/mecab-ko/downloads/


2. 파일을 다운받아서 특정 디렉토리에 저장 하고 압축을 풀어 줍니다.

tar -zxvf mecab-*-ko-*.tar.gz


3. 해당 디렉토리로 이동하여 configure/make/make install 을 진행 합니다.

cd mecab-0.996-ko-0.9.2
./configure
make
make check
sudo make install


4. 설치 버전을 확인하면 아래와 같은 오류가 발생 합니다.

mecab --version


5. 라이브러리를 로딩해주고 다시 버전을 확인하면 정상적으로 표시 됩니다.

sudo ldconfig


** 이 방법 외에 아래 명령어를 입력하면 한번에 설치 할 수도 있습니다.

pip install python-mecab-ko



 

6. 다음은 한국어 사전을 설치해 보겠습니다.

우선 사전의 최신 버전을 다운받아 마찬가지로 압축을 풀어 줍니다.

현재의 최신 버전은 mecab-ko-dic-2.1.1-20180720.tar.gz 이군요.

https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/

tar -zxvf mecab-ko-dic-2.1.1-20180720.tar.gz



7. 압축을 푼 디렉토리로 이동하여 make를 진행합니다.

cd mecab-ko-dic-2.1.1-20180720
./configure
make
sudo make install



8. 테스트를 해봅니다. Khaiii처럼 아래 명령어를 실행한 후 분석하고자 하는 문장을 입력하면 됩니다.

mecab -d /usr/local/lib/mecab/dic/mecab-ko-dic



9. Python에서 잘 되는지 테스트 해 봅니다.

import mecab
mecab = mecab.MeCab()

mecab.morphs('영등포구청역에 있는 맛집 좀 알려주세요.')
['영등포구청역', '에', '있', '는', '맛집', '좀', '알려', '주', '세요', '.']




## Anaconda Sync
$ vi /etc/ld.so.conf --> /usr/local/lib 추가

$ sudo ldconfig --> 추가한 /usr/local/lib 이하 라이브러리를 로딩하도록

$ ldconfig -p | grep libmecab

--> libmecab.so.2 (libc6,x86-64) => /usr/local/lib/libmecab.so.2

     libmecab.so (libc6,x86-64) => /usr/local/lib/libmecab.so

이렇게 두 줄이 나오면 성공


