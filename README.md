# Javascript-Pagination-Layout

An Example Pagination layout for Page or Table, [Demo](https://jsfiddle.net/8ztgrv6h/)

It transform long pagination like

![long pagination](https://user-images.githubusercontent.com/760764/193204082-f6f204dd-43fb-42a9-b010-c4ce80e89fb3.png)

into 

![short pagination](https://user-images.githubusercontent.com/760764/193204192-09cab09a-0668-4363-9511-2c535c2a59e3.png)

![paginatin layout](https://user-images.githubusercontent.com/760764/193204241-a95b6138-8181-45c4-a3c4-fef9c22d1da0.png)

![javascript pagination](https://user-images.githubusercontent.com/760764/193204275-4a449eff-8460-422f-a266-e763f66f8e57.png)

The code

```html
<html lang="en">

<head>
    <title>Javascript Pagination layout</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.0.0/dist/css/bootstrap.min.css">
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.6.1/dist/jquery.min.js"></script>
</head>

<body>
    <h3 id="h3" class="border p-2">Not yet clicked</h3>
    <ul class="pagination"></ul>

    <script>
        let totalPages = 77;
        let itemPages = getPageArray(1, totalPages)
        buildPagination(1, itemPages)

        $('ul.pagination').on('click', '.page-link', (e) => {
            let self = $(e.target)
            let parent = self.parent()
            let clickedNumber = parseInt(self.text().trim())
            $('.page-item').removeClass('active')
            h3.textContent = `Clicked: ${clickedNumber}`
            if ([parent.prev().text().trim(), parent.next().text().trim()].includes('...'))
                buildPagination(clickedNumber, getPageArray(clickedNumber, totalPages))
            else
                parent.addClass('active')
        })

        function getPageArray(currentNumber, totalItem) {
            let pageArray = []
            if (totalItem < 10) {
                pageArray = [...Array(totalItem).fill().map((_, i) => i + 1)];
            }
            else {
                if (currentNumber < 6)
                    pageArray = [...Array(7).fill(0).map((_, i) => i + 1), '...', totalItem];
                else if (currentNumber > 5 && currentNumber < (totalItem - 5))
                    pageArray = [1, '...', ...Array(5).fill().map((_, i) => i + currentNumber - 2), '...', totalItem]
                else
                    pageArray = [1, '...', ...Array(7).fill(0).map((_, i) => totalItem - i).sort()]
            }
            return pageArray
        }

        function buildPagination(index = 0, pages = []) {
            let = pagination = ``;
            for (let i = 0; i < pages.length; i++) {
                let isActive = pages[i] == index ? 'active' : '';
                let isDisabled = pages[i] == '...' ? 'disabled' : '';
                pagination += `<li class="page-item ${isActive} ${isDisabled}"><span role="button" class="page-link">${pages[i]}</span></li>`
            }

            $('ul.pagination').html(pagination)
        }
    </script>
</body>

</html>
```

#javascript #jQuery
