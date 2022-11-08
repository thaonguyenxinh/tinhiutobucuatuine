<! DOCTYPE html >
< html  lang = " en " >
< đầu >
    < meta  charset = " UTF-8 " >
    < meta  http-equiv = " X-UA-Tương thích " content = " IE = edge " >
    < meta  name = " viewport " content = " width = device-width, initial-scale = 1.0 " >
    < title > Tài liệu </ title >
    < style >
        canvas {
            vị trí : tuyệt đối;
            trái :  0 ;
            đầu :  0 ;
            chiều rộng :  100 % ;
            chiều cao :  100 % ;
            background-color :  rgba ( 0 ,  0 ,  0 ,  .2 );
        }
    </ style >
</ head >
< body >
    < canvas  id = " heart " > </ canvas >

    < script >
        cửa sổ . requestAnimationFrame  =
            cửa sổ . __requestAnimationFrame  ||
            cửa sổ . requestAnimationFrame  ||
            cửa sổ . webkitRequestAnimationFrame  ||
            cửa sổ . mozRequestAnimationFrame  ||
            cửa sổ . oRequestAnimationFrame  ||
            cửa sổ . msRequestAnimationFrame  ||
            ( hàm  ( )  {
                 hàm  trả về ( gọi lại ,  phần tử )  {
                    var  lastTime  =  phần tử . __lastTime ;
                    if  ( lastTime  ===  undefined )  {
                        lastTime  =  0 ;
                    }
                    var  currTime  =  Ngày . ngay ( ) ;
                    var  timeToCall  =  Toán học . max ( 1 ,  33  -  ( currTime  -  lastTime ) ) ;
                    cửa sổ . setTimeout ( callback ,  timeToCall ) ;
                    phần tử . __lastTime  =  currTime  +  timeToCall ;
                } ;
            } ) ( ) ;
        cửa sổ . isDevice  =  ( / android | webos | iphone | ipad | ipod | blackberry | iemobile | opera mini / i . test ( ( ( điều hướng . userAgent  ||  điều hướng . nhà cung cấp  ||  cửa sổ . opera ) ) . toLowerCase ( ) ) ) ;
        var  load  =  false ;
        var  init  =  function  ( )  {
            if  ( được tải )  trở lại ;
            được nạp  =  true ;
            var  mobile  =  window . isDevice ;
            var  koef  =  điện thoại di động ? 0,5 : 1 ;
            var  canvas  =  document . getElementById ( 'tim' ) ;
            var  ctx  =  canvas . getContext ( '2d' ) ;
            var  width  =  canvas . width  =  koef  *  innerWidth ;
            var  height  =  canvas . chiều cao  =  koef  *  innerHeight ;
            var  rand  =  Toán học . ngẫu nhiên ;
            ctx . fillStyle  =  "rgba (0,0,0,1)" ;
            ctx . fillRect ( 0 ,  0 ,  width ,  height ) ;

            var  heartPosition  =  function  ( rad )  {
                // return [Math.sin (rad), Math.cos (rad)];
                return  [ Toán học . pow ( Math . sin ( rad ) ,  3 ) ,  - ( 15  *  Math . cos ( rad )  -  5  *  Math . cos ( 2  *  rad )  -  2  *  Math . cos ( 3  *  rad )  -  Math . cos ( 4  *  rad ) )] ;
            } ;
            var  scaleAndTranslate  =  function  ( pos ,  sx ,  sy ,  dx ,  dy )  {
                return  [ dx  +  pos [ 0 ]  *  sx ,  dy  +  pos [ 1 ]  *  sy ] ;
            } ;

            cửa sổ . addEventListener ( 'thay đổi kích thước' ,  function  ( )  {
                chiều rộng  =  canvas . width  =  koef  *  innerWidth ;
                chiều cao  =  canvas . chiều cao  =  koef  *  innerHeight ;
                ctx . fillStyle  =  "rgba (0,0,0,1)" ;
                ctx . fillRect ( 0 ,  0 ,  width ,  height ) ;
            } ) ;

            var  traceCount  =  điện thoại di động ? 20 : 50 ;
            var  pointsOrigin  =  [ ] ;
            var  i ;
            var  dr  =  di động ? 0,3 : 0,1 ;
            for  ( i  =  0 ;  i  <  Math . PI  *  2 ;  i  + =  dr )  pointsOrigin . đẩy ( scaleAndTranslate ( heartPosition ( i ) ,  210 ,  13 ,  0 ,  0 ) ) ;
            for  ( i  =  0 ;  i  <  Math . PI  *  2 ;  i  + =  dr )  pointsOrigin . push ( scaleAndTranslate ( heartPosition ( i ) ,  150 ,  9 ,  0 ,  0 ) ) ;
            for  ( i  =  0 ;  i  <  Math . PI  *  2 ;  i  + =  dr )  pointsOrigin . push ( scaleAndTranslate ( heartPosition ( i ) ,  90 ,  5 ,  0 ,  0 ) ) ;
            var  heartPointsCount  =  pointsOrigin . chiều dài ;

            var  targetPoints  =  [ ] ;
            var  xung  =  function  ( kx ,  ky )  {
                for  ( i  =  0 ;  i  <  pointsOrigin . length ;  i ++ )  {
                    targetPoints [ i ]  =  [ ] ;
                    targetPoints [ i ] [ 0 ]  =  kx  *  pointsOrigin [ i ] [ 0 ]  +  width  /  2 ;
                    targetPoints [ i ] [ 1 ]  =  ky  *  pointsOrigin [ i ] [ 1 ]  +  height  /  2 ;
                }
            } ;

            var  e  =  [ ] ;
            for  ( i  =  0 ;  i  <  heartPointsCount ;  i ++ )  {
                var  x  =  rand ( )  *  width ;
                var  y  =  rand ( )  *  height ;
                e [ i ]  =  {
                    vx : 0 ,
                    vy : 0 ,
                    R : 2 ,
                    tốc độ : rand ( )  +  5 ,
                    q : ~ ~ ( rand ( )  *  heartPointsCount ) ,
                    D : 2  *  ( i  %  2 )  -  1 ,
                    lực : 0,2  *  rand ( )  +  0,7 ,
                    f : "hsla (0,"  +  ~ ~ ( 40  *  rand ( )  +  60 )  +  "%,"  +  ~ ~ ( 60  *  rand ( )  +  20 )  +  "%, 3)" ,
                    dấu vết : [ ]
                } ;
                for  ( var  k  =  0 ;  k  <  traceCount ;  k ++ )  e [ i ] . dấu vết [ k ]  =  {  x : x ,  y : y  } ;
            }

            var  config  =  {
                traceK : 0,4 ,
                timeDelta : 0,01
            } ;

            var  time  =  0 ;
            var  loop  =  function  ( )  {
                var  n  =  - Toán học . cos ( thời gian ) ;
                xung ( ( 1  +  n )  *  .5 ,  ( 1  +  n )  *  .5 ) ;
                time  + =  ( ( Math . sin ( time ) )  <  0 ? 9 : ( n  >  0.8 ) ? .2 : 1 )  *  config . timeDelta ;
                ctx . fillStyle  =  "rgba (0,0,0, .1)" ;
                ctx . fillRect ( 0 ,  0 ,  width ,  height ) ;
                for  ( i  =  e . length ;  i - ; )  {
                    var  u  =  e [ i ] ;
                    var  q  =  targetPoints [ u . q ] ;
                    var  dx  =  u . dấu vết [ 0 ] . x  -  q [ 0 ] ;
                    var  dy  =  u . dấu vết [ 0 ] . y  -  q [ 1 ] ;
                    var  length  =  Toán học . sqrt ( dx  *  dx  +  dy  *  dy ) ;
                    if  ( 10  >  length )  {
                        nếu  ( 0,95  <  rand ( ) )  {
                            u . q  =  ~ ~ ( rand ( )  *  heartPointsCount ) ;
                        }
                        khác  {
                            if  ( 0,99  <  rand ( ) )  {
                                u . D  * =  - 1 ;
                            }
                            u . q  + =  u . D ;
                            u . q  % =  heartPointsCount ;
                            if  ( 0  >  u . q )  {
                                u . q  + =  heartPointsCount ;
                            }
                        }
                    }
                    u . vx  + =  - dx  /  length  *  u . tốc độ ;
                    u . vy  + =  - dy  /  length  *  u . tốc độ ;
                    u . dấu vết [ 0 ] . x  + =  u . vx ;
                    u . dấu vết [ 0 ] . y  + =  u . vy ;
                    u . vx  * =  u . lực lượng ;
                    u . vy  * =  u . lực lượng ;
                    for  ( k  =  0 ;  k  <  u . trace . length  -  1 ; )  {
                        var  T  =  u . dấu vết [ k ] ;
                        var  N  =  u . dấu vết [ ++ k ] ;
                        N. _ x  - =  cấu hình . traceK  *  ( N. x - T. x ) ; _ _  
                        N. _ y  - =  cấu hình . traceK  *  ( N. y - T. y ) ; _ _  
                    }
                    ctx . fillStyle  =  u . f ;
                    for  ( k  =  0 ;  k  <  u . trace . length ;  k ++ )  {
                        ctx . fillRect ( u . trace [ k ] . x ,  u . trace [ k ] . y ,  1 ,  1 ) ;
                    }
                }
                //ctx.fillStyle = "rgba (255,255,255,1)";
                // for (i = u.trace.length; i--;) ctx.fillRect (targetPoints [i] [0], targetPoints [i] [1], 2, 2);

                cửa sổ . requestAnimationFrame ( vòng lặp ,  canvas ) ;
            } ;
            vòng lặp ( ) ;
        } ;

        var  s  =  tài liệu . trạng thái sẵn sàng ;
        if  ( s  ===  'hoàn thành'  ||  s  ===  'đã tải'  ||  s  ===  'tương tác' )  init ( ) ;
         tài liệu khác . addEventListener ( 'DOMContentLoaded' ,  init ,  false ) ;
    </ script >
</ body >
</ html >
