# jsonp-
jsonp前后端代码实现
后端：public class MyService : IHttpHandler
    {
        public void ProcessRequest(HttpContext context)
        {
            //获取回调函数名
            string callback = context.Request.QueryString["callback"];
            //json数据
            string json = "{\"name\":\"chopper\",\"sex\":\"man\"}";

            context.Response.ContentType = "application/json";
            //输出：回调函数名(json数据)
            context.Response.Write(callback + "(" + json + ")");
        }

        public bool IsReusable
        {
            get
            {
                return false;
            }
        }
    }
   前端：
   <script type="text/javascript">
    function addScriptTag(src){
        var script = document.createElement('script');
        script.setAttribute("type","text/javascript");
        script.src = src;
        document.body.appendChild(script);
    }
    
    window.onload = function(){
        //调用远程服务
        addScriptTag("http://localhost:20002/MyService.ashx?callback=person");
        
    }
    //回调函数person
    function person(data) {
        alert(data.name + " is a " + data.sex);
    }
</script>
