---
layout: post
title:  "SpringMVC中redirect时传入的参数中文乱码"
date:   2015-12-14 20:05:09
categories: java
excerpt:  SpringMVC中redirect时传入的参数中文乱码
---

* content
{:toc}

## 问题：

`SpringMVC` 中 `redirect` 时传入的中文参数时，在另一个请求中获取时获取出的参数乱码。

	@RequestMapping(value="searchIndex.htm",method = RequestMethod.POST)
	public ModelAndView searchIndex(Model model, HttpServletRequest request, HttpServletResponse response){
		ModelAndView view = null;
		...
		view = new ModelAndView("redirect:/projects.htm?name="+condition+"&source=" + ProjectListQueryConEnum.search.getValue());
		...
		return view;
	}

当 `name` 为中文这时进入 `projects.htm` 请求后获取 `name` 的值变为乱码。
如何解决呢？
在跳转前不能把参数直接放在请求里面而是放在 `RedirectAttributesModelMap` 对象里便可以了。
	
	@RequestMapping(value="searchIndex.htm",method = RequestMethod.POST)
	public ModelAndView searchIndex(Model model,RedirectAttributesModelMap modelMap, HttpServletRequest request, HttpServletResponse response){
		ModelAndView view = null;
		...
			modelMap.addFlashAttribute("name", condition);
			view = new ModelAndView("redirect:/projects.htm?source=" + ProjectListQueryConEnum.search.getValue());
		...
		return view;
	}

之后再进入跳转后的请求里便可以直接获取 `name` 值。
	
	@RequestMapping(value="/projects.htm", method=RequestMethod.GET)
	public ModelAndView getView(Model model, HttpServletRequest request, HttpServletResponse response) {
		
		ModelAndView view = null;
		...
		Map<String, ?> map = model.asMap();
		String name = "";
		if(map != null && map.get("name") != null){
			name = (String) map.get("name");
		}
		...
		return view;
	}

这时获取的 `name` 便不是乱码了。


---