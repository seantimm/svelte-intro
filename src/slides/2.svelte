<h1>About Me</h1>

<dl>
  <dt>Name</dt>
  <dd>Sean Timm</dd>
  <dt>Employment Status</dt>
  <dd>Unknown</dd>
  <dt>Twitter</dt>
  <dd>@seantimm</dd>
  <dt>Email</dt>
  <dd>sean@seantimm.com</dd>
</dl>

<style>
  h1 {
    text-align: center;
  }

  dl {
    padding: 0;
    margin: 0;
    display: grid;
    grid-template-columns: max-content 1fr;
    grid-gap: 2px;
    border: 1px solid yellow;
  }

  dt {
    font-weight: bold;
    color: antiquewhite;
  }

  dd {
    font-style: italic;
  }

  dt,
  dd {
    background-color: black;
    padding: 1rem;
    margin: 0;
  }

  dt::after {
    content: ": ";
  }
</style>
