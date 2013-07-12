POP
===

//这是一个弹窗插件的dome
<script>
var POP_title_set = {   //弹窗需要控制的参数
     "title_1" : "您是否要了解卧龙阁职位推送服务？",
     "title_2" : "职位推送会让更多与职位相关行业的用户在第一时间看到招聘信息。",
     "title_3" : "了解卧龙阁职位推送>>", 
        
};
var P_all_data = function(p_defaultOption){//弹窗要调用的函数
    YHW_POP.NewElement(p_defaultOption),
    YHW_POP.BgAppear(p_defaultOption),
    YHW_POP.BoxAppear(p_defaultOption),
    YHW_POP.Locate(),
    YHW_POP.Status(POP_Parameter.defaultOption_no)  //取消按钮的调用
    YHW_POP._mergeOption()
};
var POP_Parameter = {   //参数集合
    defaultOption : {
         "p_draw_id" : "bomb" ,
         "p_show_hide" : "visible" ,
         "p_bg" : true,
         "_Locate"  : "center" ,
         "p_status" : "click" ,
         "p_status_id" : "submit_push",
        
    }, 
    defaultOption_no : {
             "p_draw_id" : "bomb" ,
             "p_show_hide" : "hidden" ,
             "p_bg" : true,
             "p_status" : "click",
             "p_status_id" : "bomb_no"
    },

     DrawBox_data : {   'p_locate' : false,
                        "insert_tag" : "",
                        'p_tag' : 'aside',  
                        'p_draw_id' : 'bomb', 
                        'p_draw_class' : "push pb20", 
                        'p_string' : '<p class="p_1">'+ POP_title_set.title_1 + '</p>\
                                      <p class="p_3">'+ POP_title_set.title_2 + '<br>\
                                          <a href="#" class="blue" target="_blank">'+ POP_title_set.title_3 + '</a>\
                                      </p>\
                                      <p class="p_2">\
                                          <a href="#" class="btn_yellow" id="bomb_no" onclick="">取&nbsp;消</a><a href="javascript:void(0)" class="btn_green">确&nbsp;定</a>\
                                      </p>', 
    },
};
var YHW_POP = {
    _mergeOption : function(option){
        for(key in option) POP_Parameter.defaultOption[key] = option[key];
    },

    _getKey : function(key) {
        return POP_Parameter[key];
    }
  
    GetId : function( p_id){
        return document.getElementById(p_id)
    },   
    GetClass : function( p_class){
        return document.getElementsByClassName(p_class)
    },
    Show : function( p_show_id){
        p_show_id.style.visibility = "visible";
        p_show_id.style.zoom = 1;
    },  
    Hide : function( p_hide_id){
        p_hide_id.style.visibility = "hidden";
        p_hide_id.style.zoom = -1;
    },
    BgAppear : function(p_join){  //背景的显示隐藏     
        if( p_join.p_bg == true){     //判断是否要背景
        var bg = YHW_POP.GetId("float_mask");
            bg.style.visibility = p_join.p_show_hide;
            bg.style.height = document.documentElement.scrollHeight +'px';
        }
    },
    BoxAppear : function(p_join){ 
        var draw_div = YHW_POP.GetId(p_join.p_draw_id);   
            draw_div.style.visibility = p_join.p_show_hide;
    },   
    NewElement : function (p_join){ 
    if( !YHW_POP.GetId(p_join.p_draw_id)){
         YHW_POP.DrawBox(POP_Parameter.DrawBox_data)
        }
    },
    DrawBox : function( DrawBox_data){  //网页面內绘内容
            var element = document.createElement( DrawBox_data.p_tag);
            //判断是往body添加div 还是往指定ID
            DrawBox_data.p_locate == true ? YHW_POP.GetId( DrawBox_data.insert_tag).appendChild( element) : document.body.appendChild( element);
            element.id = DrawBox_data.p_draw_id;
            element.className = DrawBox_data.p_draw_class;
            element.innerHTML =  DrawBox_data.p_string;
    },
    Locate : function(){
        if(this._Locate == "center"){
            YHW_POP.Locate_center(POP_Parameter.defaultOption);
        }else if(this._Locate == "right"){
            YHW_POP.Locate_right(event)
        }
    },
    Locate_center : function (p_join){          /*弹窗完全居中*/
            var string = this.GetId( p_join.p_draw_id);
            var window_h =  document.documentElement.clientHeight/2; 
            var box_h =  string.clientHeight/2;
            var h = window_h - box_h;
                string.style.top = h + "px";    // 弹窗离浏览器上距离
            var window_w =  document.documentElement.clientWidth/2; 
            var box_w =  string.clientWidth/2;
            var w = window_w - box_w;
                string.style.left = w + "px";   // 弹窗离浏览器左距离
    },
    Locate_right : function(p_join){
                    x = event.clientX,
                    y = event.clientY;
                    var box = this.GetId("bomb");
                    box.style.top = y +"px";
                    box.style.left = x + "px";
    },
    Status : function(){  //选择触发的方式
        if(this._getKey('p_status') == "click"){
            YHW_POP.GetId(p_join.p_status_id).onclick = this.run('click'); function(){ P_all_data(p_join)}
        }else if(p_join.p_status == "hover"){
            YHW_POP.GetId(p_join.p_status_id).onmouseover = function(){ P_all_data(p_join)}
        }
    },

    init : function(o) {
        this._mergeOption(o);
        this.Status();
    }
};

window.onresize = function(){   //随着窗口缩放调整 居中位置
    YHW_POP.Locate_center( POP_Parameter.defaultOption)
};

//YHW_POP._Locate = POP_Parameter.defaultOption._Locate;  //获取参数值

YHW_POP.show(POP_title_set);  

</script>
