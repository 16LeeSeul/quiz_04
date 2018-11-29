Quiz 04
=

모든 퀴즈는 해당 강의중에 언급된 내용에서만 국한된다.  
퀴즈 답변이 모호하다고 생각한다면 해당 이유를 적고 본인이 생각하는 답을 작성하여 제출한다.  

0_1. 해당 퀴즈 git을 fork하여 답안을 작성하시오.  
0_2. 운영진의 공지를 확인하고 알맞은 branch로 답지를 pull request를 보내시오.  
1. follow 기능을 어떤 gem으로 구현하였는가?  
    답 :   acts_as_follower 젬으로 gem 'acts_as_follower', github: 'tcocca/acts_as_follower', branch: 'master' 코드를 이용하여 구현하였다.
2. Comment 모델과 N:M 관계를 가지는 모델을 전부 쓰시오  
    답 :   song, artist, article
3. profile 유효성검사는 어떻게 하였는지 적으시오  
    답 :   rails c  해서 p.valid?를 통해 유효한 지 확인
4. 커스텀 helper를 사용한 기능은 무엇인지 모두 쓰시오 
    답 :  profile(gravatar 사용 - 프로필 이미지 공유) , jukebox(에디터 구현) 
5. 파일 업로더는 어떤 방식으로 구현하였는가  
    답 :  이미지 파일을 업로드하기 위해 carrierwave 젬을 깔고, minimagick을 깔기 위해 imagemagick을 깔았다. 
        위의 세 젬을 다 깔고, mount_uploader :image, ProfileImgUploader를 이용해 이미지를 업로드하였다.
6. controller 중 rendering view 로만 이루어진것은 무엇인지 모두 쓰시오   
    답 :   like 
7. 강의중 게시글 본문의 에디터는 어떻게 구현하였는지 쓰시오  
    답 : profile에 role을 부여하였다. 이미 profile이 만들어져 있었으므로 해당 model table에 role이라는 column을 추가해야했다.
        $ rails g migration add_role_to_profiles role:string
        으로 role column을 추가하면
      def change
        add_column :profiles, :role, :string, null: false, default: 'user' # profile 에 column 추가 
      end
    이렇게 column을 add했다는 migrate가 생기고
        그리고 나서 jukebox helper에 
    def user_editable?
        if current_user.profile.role == 'admin'
            true
        elsif current_user.profile.role == 'editor'
            true
        else
            false
        end
    end
    을 사용해 role이 admin이나 editor인 계정에서만 편집이 가능하게끔 만들었다. (이 프로젝트에서는 default는 user로 생성, seed를 통해 role을 admin이나 editor로 주었다.)
8. 댓글은 어떻게 구현하였는지 쓰시오   
    답 :  gem 'acts_as_commentable' 젬을 사용하여 구현하였다.
          젬을 깐 후 $rails g comment 로 comment model을 만든다.
          그리고 controller를 만들어서  create와 destroy action으로 댓글을 생성하고 삭제할 수 있도록 하였다.
9. 컨트롤러로 넘어오는 입력값을 어떻게 가공하여 모델로 넘겨주는지 쓰시오  
    답 :    
            private
          def set_article
            @article = Article.find(params[:id])
          end
        이런식으로 set_article(예시)을 만들어서 
        before_action으로  넘겨주었다.
10. 프로젝트의 root_url은 어디로 연결되어있는지 쓰시오
    답 : articles#index
11. article_url 의 method : get 요청에는 몇개의 html 페이지가 렌더링되있는지 적고 각각이 어떤 redering page 인지 적으시오  
    답 : 총 4개의 html 페이지
         UserUI : user의 프로필 사진과 article을 수정하거나 삭제할 수 있는 아이콘이 들어있는  rendering page
         Like : 좋아요를 누르거나 아니거나를 할 수 있고, 몇명이 좋아요를 눌렀는지 들어있는 rendering page
         comments/form : comment를 작성하는 form이 들어있는 rendering page
         comments/index : 작성된 comment를 보여주는 index가 들어있는 rendering page

12. 본인의 보조강의 워크스페이스 github repo 주소를 적으시오  
깃헙에 없다면 새로 만들어서 링크를 제출하시오   
    답 : https://github.com/16LeeSeul/Relation-app