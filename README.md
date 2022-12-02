# Three.js Mistery Cabinet

## 3DView States

### Unauthed Views
#### SignedOut Orbital Nav View
  - [ ] **Login Form**
  - [ ] **Signup View TR**
  - [ ] **Info Point TR**
### Authed Views
#### SignedIn Orbital Nav View
  - [ ] **Play View TR**
  - [ ] **Profile View TR**
  - [ ] _Search Plaza View TR*_
  - [ ] **Chat Plaza View TR**
  - [ ] **Signout View Button**
  - [ ] **Info Point TR**
#### Play View 
  - [ ] **Play Button** 
  - [ ] **Credits Buttton**
  #### Profile View 
  - [ ] Image 
  - [ ] Info
  - [ ] Bio
  - [ ] Follow/Unfollow Button
  - [ ] _Follower# Nav_*
    - [ ] _Follower List Nav_*
      - [ ] _Follower Profile View_*
  - [ ] _Following# Nav_*
    - [ ] _Following List Nav_*
      - [ ] _Following Profile View_*
  - [ ] Personal HighScores List
#### Leaderboard View
 - [ ] Various Leaderboards (Global, Friends...)
#### Search Plaza View
  - [ ] Floating SearchBar
  - [ ] Results 'Plaza' Spherical Link
   - [ ] Result Profile View
#### Chat Plaza view
  - [ ] Mutual Follow ChatRooms
  - [ ] General Chat Plaza
  - [ ] Embedded Search Plaza View
  
  Elements in _this format_* are nice-to-have's and will probably be discarded before deadline.
  
  ## Backend Implementation
  
  ### Mongo DB Atlas Collections' Models
  
  #### User
  - [ ] _id           : __ObjectId__
  - [ ] email         : __String__
  - [ ] password      : __String__
  - [ ] username      : __String__
  - [ ] image_url     : __String__
  - [ ] firstname     : __String__
  - [ ] lastname      : __String__
  - [ ] bio           : __String__
  - [ ] followed      : __ObjectId[]__
  - [ ] following     : __ObjectId[]__
  
  #### GameRecord
  - [ ] _id           : __ObjectId__
  - [ ] _user_id      : __ObjectId__
  - [ ] _game_id      : __Integer__
  - [ ] points        : __Integer__
  - [ ] level         : __Integer__
  - [ ] time          : __Float__
  
  #### Chat
  - [ ] _id           : __ObjectId__
  - [ ] _party_ids    : __ObjectId[]__
  - [ ] history       : __Message[]__
  
  #### Message
  - [ ] text          : __String__
  - [ ] timestamp     : __Date__
  - [ ] _user_id      : __ObjectId__
  
  ### API Routes
  
  #### How authorization will work
  
  1) __client-side__ socket.emit('loginAttempt', formdata);
  2) __server-side__ socket.on('loginAttempt' (formdata) => { let user_id, token = validateLogin(formadata) })
    
    3) if request was validated:
  
    3a) socket.join('authed'); 
        socket.join(':id'); 
        authed.add(user_id, token); 
        io.to(':id').emit('authed', token);
        
    else
    
    3b) nothing is emitted
  
  
  Server-Side only authentication model:
  Dictionary<_user_id, token> authed
  
  #### User Routes
  - [ ] _/_ - __GET__ authed user                             (AUTHED)
  - [ ] _/:id_ - __GET__ user by id                           (AUTHED)
  - [ ] _/search/:query_ - __GET__ users by query             (AUTHED)
  - [ ] _/register_ - __POST__ new user                       ()
  - [ ] _/edit_ - __PUT__ existing user                       (AUTHED)
  - [ ] _/follow/:id_ - __PUT__ existing users                (AUTHED)
  - [ ] _/unfollow/:id_ - __PUT__ existing users              (AUTHED)
  - [ ] _/delete - __DELETE__ existing user                  (AUTHED)
  
  #### Record Routes
  - [ ] _/_ - __GET__ authed user records                                       (AUTHED) 
  - [ ] _/_ - __POST__ register a new score                                     (AUTHED)
  - [ ] _/:id_ - __GET__ user records by user_id                                (AUTHED)
  - [ ] _/:game/:level_ - __GET__ records by game and level                     (AUTHED)
  - [ ] _/friends/:game/:level_ - __GET__ friends' records by game and level    (AUTHED) 
  
  #### Chat Routes
  - [ ] _/_ - __GET__ all authed user's chat rooms                              (AUTHED)
  - [ ] _/:id_ - __GET__ a specific chat room by id                             (AUTHED, OWNED)
  - [ ] _/add/:chat_id/:user_ids_ - __PUT__ party members or create new chat    (AUTHED)
  - [ ] _/:id/message_ - __PUT__ a new message in the history                   (AUTHED, OWNED)
