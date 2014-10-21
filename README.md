##golang 版中文分词包, inspired from 盘古分词

###fork自 : https://github.com/chuanyi/gosegment


###修改说明
#####修改代码结构，使代码可以go get使用

###使用说明:
####  第一步: go get github.com/feimyy/gosegment
####  第二步: 到盘古分词官方网站下载[最新词典](http://pangusegment.codeplex.com/releases/view/50811)
####  第三步: 分词前初始化字典路径

    import (
    segment "github.com/feimyy/gosegment"
    "log"
    )
    
    var segHandler segment.Segment
    func main() {
    
        //......
        
        segHandler = segment.NewSegment()
        err := segHandler.Init(path) //path为字典文件的路径,通常在下载的字典文件的dicts目录下
        if err != nil {
            log.Fatalln("Failed to init segment handler", err)
        }
        
        //......
    }
   
#### 第四步: 在需要分词的地方分词
    func Segment (key string) string {
    
        //......
        
        searchKey = strings.TrimRight(searchKey, "|") + ")" 
        segs := segHandler.DoSegment(key)
        for cur := segs.Front(); cur != nil; cur = cur.Next() {
        word := cur.Value.(*dict.WordInfo)
        if word.Word != "的" {
            searchKey += word.Word + "|"
        }
        
        //......
    }