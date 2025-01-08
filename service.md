- 상품을 저장하고 상품 화면으로 리다이렉트 하는 것은 올바름
- 그런데 고객 입장에서 저장이 잘 된 것인지 안 된 것인지 확신이 들지 않음

-> 저장이 잘 되었으면 상품 상세 화면에 "저장되었습니다"라는 메시지를 보여달라는 요구사항

***
##  리다이렉트 할 때 간단히 status=true 를 추가

```java
@PostMapping("/add")
 public String addItemV6(Item item, RedirectAttributes redirectAttributes) {

     Item savedItem = itemRepository.save(item);
     redirectAttributes.addAttribute("itemId", savedItem.getId());
     redirectAttributes.addAttribute("status", true);
     return "redirect:/basic/items/{itemId}";
}
```

`RedirectAttributes` 를 사용하면 URL 인코딩도 해주고, `pathVariable` , 쿼리 파라미터까지 처리해준다.

- `redirect:/basic/items/{itemId}`
- pathVariable 바인딩: `{itemId}`
- 나머지는 쿼리 파라미터로 처리: `?status=true