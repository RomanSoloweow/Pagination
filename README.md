# Pagination

![paginator](https://user-images.githubusercontent.com/29205560/105506959-ae7db800-5cdb-11eb-98c2-26469566dc1e.png)

## Algorithm code
``` c#
int countRecords = ...;
int countOnPage = ...;
int currentPage = ...;
    
if (countRecords > 0 && countOnPage > 0)
{
    int pageSkip = currentPage-1;//how many pages are skipped
    int countPages = (int)Math.Ceiling((countRecords / 1.0) / countOnPage); //how many pages
    int countOtherPage = countPages - currentPage;//how many pages are ahead

    int step = 2;//Indent to the left and right of the current page in the center block
    int stepLeft = 2;//size of left part
    int stepRight = 2;//size of right part

    //Left and right values calculation
    int left = (pageSkip >= step) ? step : pageSkip % (step);
    int right = (countOtherPage >= step) ? step : countOtherPage % (step);

 
    if (left + right < countPages - 1)
    {
        // if not enough on the left - add on the right (so that there are always 2 * step + 1 pages)
        if (left < step)
        {
            int diff = step - left;
            diff = ((countOtherPage >= (right + diff)) ? diff : countOtherPage - diff);
            right += diff > 0 ? diff : 0;
        }

       // if not enough on the right - add on the left (so that there are always 2 * step + 1 pages)
        if (right < step)
        {
            int diff = step - right;
            diff = (pageSkip >= (left + diff)) ? diff : pageSkip - diff;
            left += diff > 0 ? diff : 0;
        }
    }

    //Go to page button
    if (countPages > (2 * step + 1))//if not all pages fit into the central panel
    {
        //Here you create go to page button with input
    }

    //Left part
    if (pageSkip > left)
    {
        int diff = (pageSkip >= (step + stepLeft)) ? stepLeft : (pageSkip - step);

        for (int i = 1; i < 1 + diff; i++)
        {
          //Here you create buttons with a redirect to the i-th page
        }

       //here <a>...</a>
    }

    //Middle part
    @if (countPages > 1)
    {
        for (int i = currentPage - left; i <= currentPage + right; i++)
        {
            //Here you create buttons with a redirect to the i-th page
        }
    }

    //Right part
    if(countOtherPage> right)
    {
        //here <a>...</a>
        int diff = (countOtherPage >= (step + stepRight)) ? stepRight : (countOtherPage - step);
        for (int i = countPages - diff + 1; i <= countPages; i++)
        {
            //Here you create buttons with a redirect to the i-th page
        }
    }
}
``` 