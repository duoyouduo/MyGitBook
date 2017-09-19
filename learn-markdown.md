学习并测试markdown语法
=====================

[I'm an inline-style link](https://www.google.com)

[I'm an inline-style link with title](https://www.google.com "Google\'s Homepage")

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[I'm a relative reference to a repository file](../blob/master/LICENSE)

This is [an example] [id] reference-style link.

[id]: http://example.com/ "Optional Title Here"
[Arbitrary case-insensitive reference text]: http://www.baidu.com

[a link](http://www.baidu.com "google")

![imgdff](/imgs/2017-07-06_155706.png "Optional title")

![Funny cat](http://cats.ru/wp-content/uploads/2017/07/46-n.jpg "Share this")

	@RequestMapping(value="/hq1")
		public ModelAndView hu(HttpSession session){
			ModelAndView mav = new ModelAndView("welcome");
			session.setAttribute("jihe", grs);
			return mav;
		}





```java
package com.jbit.controller;

import java.io.File;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpSession;

import org.apache.commons.io.FileUtils;
import org.apache.commons.io.FilenameUtils;
import org.apache.commons.lang.math.RandomUtils;
import org.aspectj.util.FileUtil;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.multipart.MultipartFile;
import org.springframework.web.servlet.ModelAndView;

import com.jbit.entity.Grade;

@Controller
public class GradeController {
	// Ò»´ÎÇëÇóÊµ¼ÊÉÏºÍ¸ÃÀàµÄÒ»¸ö·½·¨Ê±¶ÔÓ¦µÄ
	List<Grade> grs = new ArrayList<Grade>();

	@RequestMapping(value="/hq")
	// Grade ÊµÌåÀàÖÐÇ°ÈýÁÐÖµÊÇ×Ô¶¯¸³ÖµÉÏÈ¥µÄ£¬µÚËÄÁÐÒª¸ù¾ÝÓÃ»§µÄÊäÈëÈ¥ÄÃÖµ
	public String Hql1(Grade g,
			@RequestParam(value="file_pic") MultipartFile attach,HttpSession hs){
      // 1.ÎÒÃÇÒªÔÚ·þÎñÆ÷ÉÏ´´½¨Ò»¸öÎÄ¼þ¼Ð
	  // 2. »ñÈ¡ÎÄ¼þµÄÂ·¾¶
		String path = hs.getServletContext().getRealPath("/upload");
		// 3. »ñÈ¡ÎÄ¼þÃû×Ö ¿Í»§¶ËÉÏ´«µÄÎÄ¼þÃû
		String fileName = attach.getOriginalFilename();
		// ÎªÁË·ÀÖ¹²»Í¬¿Í»§ÉÏ´«ÎÄ¼þÍ¬Ãû£¬ÎÒÃÇ½«²»»áÊ¹ÓÃ¿Í»§¶ËÉÏ´«µÄÎÄ¼þÃû£¬¶ø×Ô¶¨ÒåÎÄ¼þÃû
		String newfileName=System.currentTimeMillis()+
				RandomUtils.nextInt(1000000)+"_Personal.jpg";
		System.out.println(newfileName);
		
		// ¸ù¾Ý¾ÉÎÄ¼þÃû»ñÈ¡ºó×ºÃû
		String houzhui =FilenameUtils.getExtension(fileName);
		System.out.println(houzhui);
		if(houzhui.contains("jpg")||houzhui.contains("png")){
			// ½«¿Í»§¶ËÉÏ´«µÄÎÄ×ÖÃû´æ·Åµ½Êý¾Ý¿â
			g.setGradeUrl(fileName);
			// 4.´´½¨ÎÄ¼þ¶ÔÏó
			File f = new File(path,newfileName);
			
			try {
				attach.transferTo(f);
			} catch (IllegalStateException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
		}else{
			System.out.println("ÎÄ¼þ¸ñÊ½´íÎó£¬²»ÔÊÐíÉÏ´«");
		}
		
		
		//       grs.add(g);
       return "redirect:hq1";
	}
	
	@RequestMapping(value="/delete/{id}")
	public String shanchu(@PathVariable Integer id){
		System.out.println(id);
		return "index";
	}
}
```